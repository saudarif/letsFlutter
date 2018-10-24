
## There is an Object class.

### toString

Everything, even a number, function or ```null``` they all are objects. And each of these objects are derived from the ```Object``` class. That is the reason that we can call a function ```toString()``` on an ```int```, a ```double```, etc. as the function ```toString()``` is present in the ```Object``` class.

In the example below we can see that how we can easily convert couple of ```double``` objects to strings. And also at the last line of ```main()``` we can see how we can use ```toString()``` on a function object too.

```
class Superhero {
  String getPowerlevel(double strength, double speed) {
    double powerLevel = strength * speed;

    String powerLevelText = "Strength :" +
        strength.toString() +
        "\nSpeed :" +
        speed.toString() +
        "\nPowerLevel :" +
        ((powerLevel > 9000) ? "It's Over 9000!" : powerLevel.toString());

    return powerLevelText;
  }
}

main() {
  Superhero superman = Superhero();
  print(superman.getPowerlevel(7000.0, 2000.0)); // Deep apology to Superman haters, but really "It's Over 9000!"

  print(superman.getPowerlevel.toString());
}
```

The output will be...
```
Strength :70
Speed :20
PowerLevel :1400
Closure 'getPowerlevel$2' of Instance of 'Superhero'
```


### Have you heard about noSuchMethod ?

```Object``` class has a method called ```noSuchMethod``` This method is Invoked when a non-existent method or property is accessed on an object and the default behavior is to throw a NoSuchMethodError. But Classes can override noSuchMethod to provide custom behavior. If a value is returned, it becomes the result of the original invocation.

Lets check out an example. 

```
class Superhero {
  dynamic noSuchMethod(Invocation invocation) {
    
      if(invocation.isMethod){
        print(invocation.namedArguments);
      }
    
  }
}

main() {
  Superhero superman = Superhero();
  (superman as dynamic).getPowerlevel(strength:7000.0, speed:2000.0);
}
```
The output will be ```{Symbol("speed"): 2000, Symbol("strength"): 7000}```.

We can do more complex operations but we will need ```dart:mirrors``` package, which is not currently included in flutter package. So... lets not go there.

### hashCode 

```Object``` class has another importaint property, a read-only property, called as hashCode. A hash code is a single integer which represents the state of the object that affects operator == comparisons. 

The default hash code works the same way as the default ```operator ==``` implementation. It only considers objects equal if they are identical.

Hash codes must be the same for objects that are equal to each other according to operator ==. But Objects that are not equal are allowed to have the same hash code.
A good rule to live by is that If you are overriding ```hashCode```, you should also override the ```operator ==``` to maintain consistency.

Lets see a good way to override these properties.

```
class Superhero {
  
  String name;
  double speed;
  double strength;
  
  Superhero(this.name, this.speed, this.strength);

  bool operator ==(o) => o is Superhero && o.name == name && o.speed == speed && o.strength == strength;
  int get hashCode => name.hashCode ^ speed.hashCode ^ strength.hashCode;
}

main() {
  Superhero superman = Superhero('Clark Kent', 2000.0, 300.0 );
  print(superman.hashCode);
}
```

Output will be ```331963414```

