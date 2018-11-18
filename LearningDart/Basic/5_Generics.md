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

On more general terms we can follow follow the example below to restrict genric parameters.

```
class Foo<T extends SomeBaseClass> {
  // Implimentation ...
}

class Extender extends SomeBaseClass {...}

//It’s OK to use SomeBaseClass or any of its subclasses as generic argument:

var someBaseClassFoo = Foo<SomeBaseClass>();
var extenderFoo = Foo<Extender>();

//It’s also OK to specify no generic argument:

var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```

### More than one genric parameters

We can have more than one generic parameters in a generic function or a generic class.

```
Map<K, V> singletonMap<K, V>(K key, V value) {
  return <K, V>{ key, value };
}
```

### Generic in 'function-typed parameters', 'local functions', and 'function expressions'

Lets see a generic method as a parameter.

```
void functionTypedParameter(T callback<T>(T thing)) {}
```

And a local generic function.

```
void localFunction() {
  T itself<T>(T thing) => thing;
}
```

Also we can create a generic function expression to a local variable.

```
void functionExpression() {
  var lambda = <T>(T thing) => thing;
}
```
