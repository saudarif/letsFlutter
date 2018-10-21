#  Points To Remember - What makes Dart different from others.

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

## I have seen Asserts

The ```assert()``` call is ignored in production code. During development, ```assert(condition)``` throws an exception unless condition is true. 


## Dart can infer types

Remember that Dart is a strongly typed language. So we can define variables in the following ways.

### Defining variables

Defining variables is simple, same as many languages.
```
String name = 'Clark Kent';
```

If an object is not restricted to a single type we can define it as ```dynamic``` type or ```Object``` type. Its a flexibility that you get in a dynamic language.
```
dynamic name = 'Clark Kent';

(foo as dynamic).bar(); //valid. compiler won't check if bar() exists
```

But you can also infer types. That is usefull if you do not want to explicitly define the type of a variable.
```
var name = 'Clark Kent';
```

But remember that using ```var``` to define variables will make the variable type as ```dynamic```. So we can do this too.
```
var name = 'Clark Kent';
name = 123; //Works fine....
```

### default value.

Uninitialized variables have an initial value of ```null```. Even numbers.

### Defining Constants

for that we can use ```final``` or ```const``` to define the variable. A ```final``` variable can be set only once; a ```const``` variable is a compile-time constant. ```const``` variables are implicitly final.

Instance variables can be ```final``` but not ```const```. Final instance variables must be initialized before the constructor body starts. Static variables of a class can be both ```const``` or ```final```.
```
class Superhero {
  final name;
  static const description = 'a Superhero';

  Superhero(this.name);
}
```

Difference between ```const``` and ```final```?

- final variable is initialized when accessed.
- const is internally final in nature but the main difference is that its compile time constant which is initialized during compilation.

This means that following code will work fine with ```final``` but not with ```const```.
```
final name = defaultName();
const nickName = defaultName(); //Error : Method invocation is not a constant expression.

String defaultName(){
    return 'Bruce Wane';
}
```

### constant values

```const``` keyword can also be used to create constant values.
```
var superheros = ['Superman', 'Batman'];
var superheroines = const ['Wonder Woman'];
main() {
  superheros.add('Flash');
  print(superheros);                  //Prints : [Superman, Batman, Flash]
  superheroines.add('Black Canary');  //Error  : Unsupported operation: add
}
```

## Generics

The most basic example of a generic class that you can find in Dart is array type, that is called as ```List```. It will look like - ```List<E>```.
By convention, In Dart, type variables have single-letter names, such as E, T, S, K, and V.

```
var superheros = List<String>();
superheros.addAll(['Superman', 'Batman', 'Flash']);
```

### Generic Class
Lets see how can we create a Generic class.

```
class Pair<E> {
 	var values = List<E>(2);
  
  Pair (E first, E second)
  {
    values[0]=first; values[1]=second;
  }
}

main() {
  var stringPair = Pair<String>('hi', 'hello');
  print(stringPair.values);
  
  var intPair = Pair<int>(10, 20);
  print(intPair.values);
}
```

### Generic function
We can also creat a generic function. Lets see an example.

```
E middleElement<E>(List<E> collection){
  int mid = (collection.length/2).floor();
  assert(collection.length > 0);
  return collection[mid];
}

main() {
  print(middleElement([10,20,30])); //Output : 20
}
```

### Typed Collection Literals

We can define Typed Collection as ```<E>[]``` for array and ```<E, F>{}``` for map, where E and F are types. Lets see a better example.

```
var superHeros = <String>['superman', 'flash'];
var powers = <String, String>{
  'superman': 'strength',
  'flash': 'speed'
};
```

We can Use parameterized types with constructors like ```var names = List<String>();``` or ```var powers = Map<String, String>()```.


### Restricting the parameterized type

When implementing a generic type, you might want to limit the types of its parameters, here is how you can do that.

```
E getMax<E extends num>(E first, E second) {
  return (first.compareTo(second) < 0)?second:first;
}

main() {
  print(getMax(20,40)); //Output: 40
}
```

