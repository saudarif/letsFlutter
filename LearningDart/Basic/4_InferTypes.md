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
