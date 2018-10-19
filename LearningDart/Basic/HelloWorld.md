#  Hello World - Our first program in Dart.

Lest create our first program that will print, ```Hello World```

```
// This is where the app starts executing.
main() {
  print('Hello World'); // Print to console.
}
```

Lets talk about this program. 

The Execution of any dart program will start at main function.

## Main Function

Every app must have a ```main()``` function. ```main()``` is the entry point of the application. The return type of ```main()``` function is ```void``` and it takes an optional  ```List<String>``` argument parameter.

```
void main(List<String> arguments) {
  print(arguments);
}
```

### Command line program.
The above program will print all the arguments that are passed to the program at the time of launch. But we cannot run this program on DartPad and expect to see argument list in console. Because the DartPad does not allows us to pass arguments. So to demonstrate this we need to run the program on terminal (of mac machine) or command prompt (of windows machine). And to compile and run the program on terminal/Cmd we will need Dart VM (dart), which comes when you [install the Dart SDK](https://www.dartlang.org/tools/sdk#install).


To get Dart VM (dart) you will need DartSDK that you can install from the link above, Dart also comes with flutter package. So if you already have flutter package in your machine, you can find dart at ```<path to flutter package>/flutter/bin/cache/dart-sdk/bin```. Now we need to add this path to our environment variables using export command ```export PATH=<path to flutter package>/flutter/bin/cache/dart-sdk/bin:$PATH``` so that we can use ```dart``` command. 


Now we need to save the above program in a file printArguments.dart, and open terminal go to file's location and execute ```dart  printArguments.dart hi this is my first command line program```. And you can see the output as follows - ```[hi, this, is, my, first, command, line, program]```



