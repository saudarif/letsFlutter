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

### Execution of a dart Command line program.
The above program will print all the arguments that are passed to the program at the time of launch. But we cannot run this program on DartPad and expect to see argument list in console. Because the DartPad does not allows us to pass arguments. So to demonstrate this we need to run the program on terminal (of mac machine) or command prompt (of windows machine). And to compile and run the program on terminal/Cmd we will need Dart VM (dart), which comes when you [install the Dart SDK](https://www.dartlang.org/tools/sdk#install).


To get Dart VM (dart) you will need DartSDK that you can install from the link above, Dart also comes with flutter package. So if you already have flutter package in your machine, you can find dart at ```<path to flutter package>/flutter/bin/cache/dart-sdk/bin```. Now we need to add this path to our environment variables using export command ```export PATH=<path to flutter package>/flutter/bin/cache/dart-sdk/bin:$PATH``` so that we can use ```dart``` command. 


Now we need to save the above program in a file printArguments.dart, and open terminal go to file's location and execute ```dart  printArguments.dart hi this is my first command line program```. And you can see the output as follows - ```[hi, this, is, my, first, command, line, program]```

## Comments

Dart Supports 3 types of comments : 
  - Single Line comments
  - Multi line comments
  - Documentation Comments

### Single Line Comments
Single line comment starts with ```//``` and ends with the end of the line

```
// This is a Single Line Comment.
```

### Multi Line Comments
Single line comment starts with ```/*``` and ends with ```*/```

```
/*
 This is a multi line comment...
  -------------------------------------------------------
  ------------------Ignored by compiler------------------
  -------------------------------------------------------
 */

 /****************************************
  * Title : Program Name *
  * Author: Author Name *
  ***************************************/
```

### Documentation Comments
The documentation comment are either a multi-line or single-line comment that begins with ```///``` or ```/**```. We generally use ```///``` on consecutive lines to create a documentation comments. Lets see some examples : 

```
/// A superhero is a type of heroic stock character, 
/// usually but not necessarily possessing supernatural or superhuman powers,
///
/// A superhero is dedicated to fighting the evil of their universe, 
/// protecting the public, and usually battling supervillains.
class Superhero {
  String name;


  // Constructor, with syntactic sugar for assignment to members.
  Superhero(this.name) {
    // Initialization code goes here.
  }

}
```

But we can do a lot more with Documentation comments. The code snippet below shows an elegent way of providing documentation for a function.

```
  /// A method to calculate the powerlevel of a superhero.
  ///
  /// [strength] is a measure of Strength of superhero.
  /// [speed] is a measure of speed of superhero.
  /// Returns a string that contains power level.
  /// Throws an [Error] if any one of either [strength] or [speed] is less than 1.
  String getPowerlevel(double strength, double speed){
    
    if(strength < 1){
      throw "Strength readings are wrong.";
    }
    
    if(speed < 1){
      throw "Speed readings are wrong.";
    }
    
    double powerLevel = strength*speed;
    
    if(powerLevel > 9000){
      return "It's Over 9000!";
    }
    
    return powerLevel.toString();
  }
```

And we can use markdown too. Markdown is a text-to-HTML conversion tool for web writers. Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML). But we should avoid using markdown excessively.

```
/// # A Header
///
/// ## A subheader
///
/// ### A subsubheader
///
///
/// Links can be:
///
/// * http://www.just-a-bare-url.com
/// * [with the URL inline](http://google.com)
/// * [or separated out][ref link]
///
/// [ref link]: http://google.com
///
/// ```html
/// <h1>HTML is magical!</h1>
/// ```
/// * Unordered lists
/// * can be created
/// * like this
///
/// 1. Numbered lists.
/// 2. Are, well, numbered.
/// 1. But the values don't matter.
///     * You can nest lists too.
/// Code blocks are fenced in triple backticks:
///
/// ```
/// this.code
///     .will
///     .retain(its, formatting);
/// ```
```

The output will be like this...

# A Header

## A subheader

### A subsubheader


Links can be:

* http://www.just-a-bare-url.com
* [with the URL inline](http://google.com)
* [or separated out][ref link]

[ref link]: http://google.com

```html
<h1>HTML is magical!</h1>
```
* Unordered lists
* can be created
* like this

1. Numbered lists.
2. Are, well, numbered.
1. But the values don't matter.
    * You can nest lists too.

    
Code blocks are fenced in triple backticks:

```
this.code
    .will
    .retain(its, formatting);
```