# JavaScript-interview-preparation
My preparation for getting a full time job as a front end developer
___________________

* NaN appears when a non-number cannot be coerced to a number.
  
  NaN is type Number

  Every Number is a float in JavaScript

  NaN compared to anything is false

* 'null' is an object

  'null' datatype qualifies as an Object.
  ```
  const bar = null;
  console.log(typeof bar === "object"); //returns true!
  ```

  If you want to reliably check if 'bar' is an object, check for 'null' condition first.
  ```
  console.log((bar !== null)&&(typeof bar === "object"));
  ```

  1. If 'bar' is a function, the above code will return `false`.
  If you want to return `true` for 'bar' being a function, simply add the following with an `and` condition
  ```
  (typeof bar === "function")
  ```
  
  2. Arrays are Objects too, so the expression will return `true` for arrays. 
  To return `false` for arrays, use the `toString.call()` method:
  ```
  (toString.call(bar) !== "[object Array]"))
  ``` 
*  Slice

  Array.slice(starting index, index before which to stop);
	  
	  	
	  "john".slice(2); //returns "h"
	  "john".slice(1,3); //returns "oh"
	  
  With a negative starting index, 'slice' offsets the array from the end by that magnitude
	  
	  
	  "john".slice(-1); //returns "n"
	  "john".slice(-2); //returns "hn"
	  
* Test if a number is an integer:
	```
	x.isInteger() //ES6
	return((x^0)===x)
	return(Math.round(x)===x)
	```
 
* Since 'toString' is defined in Object.prototype, whoever inherits Object, will by default get the 'toString' method.

  But, Array objects, override the default 'toString' method to print the array elements as comma separated string.
  [source](http://stackoverflow.com/questions/30010996/difference-between-object-prototype-tostring-callarrayobj-and-arrayobj-tostrin)
  
  toString() can be used with every object and allows you to get its class using the `call` function.
  ```
  var toString = Object.prototype.toString;

  toString.call(new Date);    // [object Date]
  toString.call(new String);  // [object String]
  toString.call(Math);        // [object Math]

  // Since JavaScript 1.8.5
  toString.call(undefined);   // [object Undefined]
  toString.call(null);        // [object Null]
  ```
  [source](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

* `var a = b = 3;` is equivalent to 
  ```
  b = 3;
  var a = b;
  ```
  
  If the statement was enclosed within a function
  
  ```
  function funk(){var a = b = 3;}
  console.log(b);// We get 3
  console.log(a);//we get undefined
  ``` 
  
  b would be accessible and defined outside the function, but a would not be defined in the global scope because it has a 'var' prefix in the declaration
  
  If the statement had 'const' instead of 'var', neither of the variables would print outside the block's scope

* Use strict
 
  Does not allow variables to default to global
 
  Does not allow this to default to global

  Yells at duplicate variable names

  Silently failing errors are exposed

* Coercion

  Type coercion means that when the operands of an operator are different types, one of them will be converted to an "equivalent" value of the other operand's type. For instance, if you do:

  ```
  boolean == integer
  ```
  the boolean operand will be converted to an integer: false becomes 0, true becomes 1. Then the two values are compared.

  However, if you use the non-converting comparison operator ===, no such conversion occurs. When the operands are of different types, this operator returns false, and only compares the values when they're of the same type.
  [source](http://stackoverflow.com/questions/19915688/what-exactly-is-type-coercion-in-javascript)
  
  Another example:
  
  ```
  [] + 5
  ```
  In JavaScript, + can mean add two numbers or concatenate two strings. In this case, we have neither two numbers nor two strings. We only have one number and an object. 
  Javascript knows how to concatenate strings, so it converts both [] and 5 into strings and the result is string value “5”.
  
  Coercion examples:
  
- Example 1: 1 + "2" + "2" Outputs: "122" Explanation: The first operation to be performed in 1 + "2". Since one of the operands ("2") is a string, JavaScript assumes it needs to perform string concatenation and therefore converts the type of 1 to "1", 1 + "2" yields "12". Then, "12" + "2" yields "122".

- Example 2: 1 + +"2" + "2" Outputs: "32" Explanation: Based on order of operations, the first operation to be performed is +"2" (the extra + before the first "2" is treated as a unary operator). Thus, JavaScript converts the type of "2" to numeric and then applies the unary + sign to it (i.e., treats it as a positive number). As a result, the next operation is now 1 + 2 which of course yields 3. But then, we have an operation between a number and a string (i.e., 3 and "2"), so once again JavaScript converts the type of the numeric value to a string and performs string concatenation, yielding "32".

- Example 3: 1 + -"1" + "2" Outputs: "02" Explanation: The explanation here is identical to the prior example, except the unary operator is - rather than +. So "1" becomes 1, which then becomes -1 when the - is applied, which is then added to 1 yielding 0, which is then converted to a string and concatenated with the final "2" operand, yielding "02".

- Example 4: +"1" + "1" + "2" Outputs: "112" Explanation: Although the first "1" operand is typecast to a numeric value based on the unary + operator that precedes it, it is then immediately converted back to a string when it is concatenated with the second "1" operand, which is then concatenated with the final "2" operand, yielding the string "112".

- Example 5: "A" - "B" + "2" Outputs: "NaN2" Explanation: Since the - operator can not be applied to strings, and since neither "A" nor "B" can be converted to numeric values, "A" - "B" yields NaN which is then concatenated with the string "2" to yield “NaN2”.

- Example 6: "A" - "B" + 2 Outputs: NaN Explanation: As exlained in the previous example, "A" - "B" yields NaN. But any operator applied to NaN with any other numeric operand will still yield NaN.  
  
- 'this' example:
  ```
  var myObject = {
      animal: "bear",
      func: function() {
          (function() {
              console.log(this.animal, this);
          }());
      }
  };
  myObject.func();
  ```
  `this` inside of a `function` will always equal the global object (`window`) unless you change the context of `this` via `.bind()`, `.call()` or `.apply()`.
  
  `this` of a function inside a function always refers to the global object, even if the outer function is contained by an object. Objects do not have an execution context.
  
  This function returns `undefined` for 'this.animal' and returns `Window` object for 'this'.
  Because 'animal' is not present in the global scope and is limited to the object, it gets a value of 'undefined'.
  If there were 'animal' in the global scope, the inner function would print the global value and not the value from the object that contains the inner function.
  
  However, if it were not a function inside a function, and instead were a function directly inside the object, then 'this.animal' would be taken from the enclosing object's 'animal'.

# All about `this`

`this` does not, in any way, refer to a function's lexical scope.

You cannot use a `this` reference to look something up in a lexical scope. 

When a function is invoked, an activation record, otherwise known as an execution context, is created. This record contains information about where the function was called from (the call-stack), how the function was invoked, what parameters were passed, etc. One of the properties of this record is the `this` reference which will be used for the duration of that function's execution.

1. `this` inside a normal function always refers to Window
	```
	function func(){console.log(this)} // We get window

	function printWord(){return this.word}
	
	const word = “Hello”; //Global word
	const callerObject = {const word: “Goodbye”};

	printWord(); //Returns Hello
  

The scope of 'this' in printWord is Window, so it accesses window.word which is “hello”


2. Using `apply()` we can explicitly set the `this` of func function to the object 
	passed as a parameter.
  
  ```
	func.apply(callerObject);// `this` becomes callerObject

	printWord.apply(callerObject); //returns “Goodbye”
  ```

3. When you use dot notation, `this` is what actually comes before the dot.
	```
	function func(){console.log(this)}
	callerObject.printWord = func;
	printWord(); // Returns callerObject as `this` 
	
.apply() has greater precedence over dot notation
	
  
	callerObject.printWord.apply(func);//'this' becomes func
	
* __If you duplicate the function and copy it. Then its lexical scope is not transferred. Because functions are objects are passed by reference. If you assign a function to a variable, its lexical scope is transferred__

	```
	func2 = callerObject.printWord;
	func2(); //returns “Hello” which is taken from the global scope and not from callerObject
	```

If we have two nested objects and a function inside the inner object, `this` of that function returns the inner object. 
When objects cascade, `this` of the contained function propagates from inside to outside one step at a time.

	var obj = {func: {
		b: function(){
			console.log(this)
			}
		}
	}

	obj.func.b();// returns {b: function}
if you try to access any variables in b, 
it would check b and if not found, then check the global execution context.
This is because the outer environment i.e the lexical scope of the function is the Global object.

4. As an object method

When a function is called as a method of an object, its this is set to the object the method is called on.

In the following example, when o.f() is invoked, inside the function this is bound to the o object.

	var o = {
	  prop: 37,
	  f: function() {
	    return this.prop;
	  }
	};

	console.log(o.f()); // logs 37
	
**Note that `this` set to an object's scope does not mean that the outer environment of the function will be the object. Objects don't have an execution context. So even if `this` of the function is set to the object scope, the outer lexical environment of the function will still be the global object because the containing object does not have an execution stack of its own.**

5. `new` keyword.
  ```
function func3(){this.word = “Hi”;} //when func3 is instantiated, it also returns `this`. It returns the newly created object
const obj2 = new func3(); 
obj2 //returns object with {word: “Hi”}
  ```
When a function is used as a constructor (with the new keyword), its `this` is bound to the new object being constructed.

A function used as getter or setter has its `this` bound to the object from which the property is being set or gotten.

When a function is called as a method of an object, its `this` is set to the object the method is called on.

The `this` binding is only affected by the most immediate member reference. The most immediate reference is all that matters.

6. Arrow functions

In arrow functions, `this` is set lexically, i.e. it's set to the value of the enclosing execution context's this. In global code, it will be set to the global object:

	var globalObject = this;
	var foo = (() => this);
	console.log(foo() === globalObject); // true

## Scoping: functions inside objects and functions inside functions

	> var tex = 1
	< undefined
	> var mex = {tex:2; func:function(){console.log(tex)}};
Mistake: did not use a comma in the object, used semi-colon instead
	
	< SyntaxError: Unexpected token ';'. Expected '}' to end an object literal.
	> var mex = {tex:2, func:function(){console.log(tex)}};
	< undefined
	> func
Mistake, tried to access member function directly

	< ReferenceError: Can't find variable: func
	> mex.func
	< function (){console.log(tex)}
	> mex.func()
	[Log] 1
	
Our function `tex` contained in `mex` object, would have its outer environment set to global scope and not the object scope.
Any function contained within a function, has its outer environment value depend upon where the inner function lexically sits. If inside the outer function, the outer environment would point to the scope of the outer function.
If not, it would point to the global environment. 

Note that where a function was called does not have an impact on the function's outer environment.
Where it lexically sits has an effect on its outer environment.
And functions in objects point to global scope because objects do not have execution environments.

BUT, if we had used `this.tex` instead of just `tex` inside the function, it would output 2.

### A subtle twist

If we were to make only one change in the `func` function, it would completely change the value logged by `func`

#### Code before

	var tex = 1;
	var mex = {tex:2, func: function(){console.log(tex);}}
	mex.func(); //returns 1

#### Code after

	var tex = 1;
	var mex = {tex:2, func: function(){console.log(this.tex);}} //here's the change
	mex.func(); //returns 2
	
In the code after, I set the console.log to `this.tex` instead of just `tex`.
Here's the progression:

- Global execution context is set up. A variable environment is set up.
- Memory is allocated to tex variable and it is set to 1.
- Memory is allocated to mex and its member variables are populated
- mex.func() is encountered. 
- An execution stack for mex.func() is set up. A variable environment for func is set up.
- func does not contain any variables of its own.
- console.log is executed, and tex is encountered.
- **In code before:** tex is not present in func. So the outer lexical environment of func is referenced.
- the lexical outer environment of func is the global context.
- The global value of tex is logged in the console.

- **In code after:** 'this.tex' is encountered. 
- 'this' of func is the containing object mex.
- The value of tex inside mex is referenced
- The local value of tex is logged in the console.

## Another tricky scenario: call by reference

	b = function (){console.log(this)}
	> var thing = b
	< undefined
	> thing
	< function (){console.log(this)}
	> var newStuff = {thing: "Hello World"}
	< undefined
	> thing
	< function (){console.log(this)}
	> newStuff
	< {thing: "Hello World"}
	> newStuff.thing
	< "Hello World"
	
Suppose we want to test out call by reference feature of objects. We have `b` inside `func` inside `obj`. We assign object `b` to a variable `thing`. We create a new object newStuff and try to assign "Hello world" to thing. Does this modify thing and hence the original `b` object? It should. But in this case, we are referring to an object containing its own local variable thing. Hence it does not explicitly reference the global thing that we had.

	var buff = [1,2,3]
	undefined
	var cuff = buff
	undefined
	cuff.pop()
	3
	cuff
	[1, 2]
	buff
	[1, 2]

Above, since arrays are objects, they are passed by reference. The buff array is modified above.
If you did not want to modify it, just copy it with the spread operator. `var cuff = [...buff]`
This won't let buff change when cuff is changed.

# Execution stack, variable environment & outer variable environment

* In an execution stack, an execution context for each function is created in the order in which they appear in the flow. However, when it comes to variable environments, each execution context maintains a link to the immediate outer (lexical) environment, where the function was written. This is the outer lexical environment, the environment in which the current function has been physically written. This outer environment is used when a variable inside our current execution context is not defined. So it is fetched from the lexically outer environment. If it doesn't find it there and there is an ever outer lexical environment, it checks for the variable there. This jumping of a variable value when it is not defined, from one environment to another, is called the **scope chain**. 

* Every execution context has its own variable environment. Every variable in JavaScript belongs to some variable environment. Global environment if it is not inside any execution context of functions. Where it is referenced from does not have an impact on its value, its lexical context has an impact on its value. 

	```
	function b(){
	console.log(myVar);
	}
	function a(){
	var myVar = 2;
	console.log(myVar); 
	b();
	}
	var myVar = 1;
	console.log(myVar);
	a();
	```
	
	Here, myVar is globally set to 1. So it prints 1.
	Then it dives into a()
	a has myVar = 2, so it prints 2.
	Then it dives into b()
	b doesn't have a myVar, so it refers immediate outer lexical environment.
	There is nothing containing b(), so it refers to the global environment.
	Finally, it prints the global value of myVar, which is 1.

* Another example:

	```
	function b(){
	var myVar;
	console.log(myVar);
	}
	function a(){
	var myVar = 2;
	console.log(myVar); 
	b();
	}
	var myVar = 1;
	console.log(myVar);
	a();
	console.log(myVar);
	```
	First, it opens the global execution context and sets a variable environment for myVar
	myVar is set to 1.
	It prints 1.
	Then a() is called and its execution context is set, and a variable environment for myVar is created.
	myVar is set to 2.
	It prints 2.
	Then b() is called, its execution context is set up and a variable environment for myVar is created in b()
	myVar is set to undefined.
	It prints undefined.
	b() ends, so its execution context is popped. a() ends, its execution context is popped.
	Now we are in the global execution context, where myVar is 1.
	So it prints 1 again.

### How are events handled by JS? / How are asynchronous calls handled by JS

- The global execution context is set up.

- 'this' is created

- Variable environment for the global execution context is set up

- Any function call that appears first from top to bottom sets up its own execution context in the execution stack

- Its variable environment is set up

- The function 'a' is run from top to bottom

- Any other function that is called back by 'a' sets up its own execution context

- Variable environment is created and the function is run from top to bottom

- The function gives back control to 'a'

- When a finishes, it gives back control to the global execution context

- The global execution context finishes up all its statements

- Any event encountered by an eventListener in the code is sent out to the event queue

**Events**

- After the execution stack is empty, the engine starts processing events one by one from the event queue

- An event is read and any function call made by the event is taken in

- The function sets up its execution context in the stack, its variable environment is set up

- The function runs and similarly, any subsequent functions are run till the execution stack is empty

- The next event in the queue is taken in, and the process continues

## The IIFE lifecycle, a friend of frameworks

- Global execution context is first created.
- Then it comes across an IIFE outer parenthesis.
- It applies the grouping operator and sees that function as an expression.
- It almost loads the function in the variable environment of the global execution context.
- But, when it comes across the second pair of parentheses, it recognizes it as a function and creates a new execution context.
- Any variable created inside the IIFE is stored in the IIFE’s variable environment, not the global scope.
- The global version of variables is not taken. The local IIFE variables are used in an IIFE.
- This avoids major conflicts, and hence IIFEs are used in major frameworks. 
- It keeps the code safe.
- So in a framework, you will usually see all code begin with an opening parenthesis and closing with a closing parenthesis.
- It does not touch the global object.
- The global object is safe.
- Unless, we explicitly pass the global object aka Window as a parameter to an IIFE and access that `global.variable` inside the IIFE. That is the only way an IIFE can touch the global context.
- An IIFE neither uses global variables nor pushes variables to the global object, given that it has all those variables locally, by default. If you explicitly supply a global variable to an IIFE or access it from an IIFE and it is accessible, and you alter that variable, then IIFEs can alter global variables.

### Precedence and associativity

	var a = 1, b = 3, c = 4;
	a = b = c;
	console.log(a,b,c);
	
Prints 4,4,4.
Because of associativity. '=' operator is right to left

- 3 < 2 < 4 returns true, because the '<' operator is left to right associative. It returns false (3 < 2) and then true (false < 4), leaving us with a 'true' result. Note that false is coerced to a value 0 which is less than 4 and hence yields true.

### By Value and by Reference

- Primitive types always get a copy - by value
	```
	var a = 3;
	var b = a; //b and a don't point to the same 3. b gets its own 3 stored in a different memory location
	```
- Objects always get reference to same object - by reference
	```
	var cars = {ford:"Ford GT", nissan:"GTR"};
	var raceCars = cars; //both point to the same object
	raceCars.hennessey = "Venom GT";
	cars; 
	//returns
	//{ford: "Ford GT", nissan: "GTR", hennessey: "Venom GT"}
	//Awesome! Isn't it?
	```
- = operator creates new memory space. It is a special case where by reference does not apply.
	```
	cars = {dodge: "Viper", mazda:"RX-7", toyota:"Supra"};
	raceCars;
	//returns
	//{ford: "Ford GT", nissan: "GTR", hennessey: "Venom GT"}
	```
	
## Closures

JS preserves the variable environment of an execution context even after that context has finished executing and is popped off the stack.

These retained variables are available to functions that are authorized to access them.

	function build(){
	var arr = [];
	for(var i=0; i<3; i++){
	arr.push(function(){console.log(i)});
	}
	return arr;
	}

	var f = build();

	f[0]();
	f[1]();
	f[2]();

- build function pushes the definition of 3 functions into array arr. 

- Note that it does not console.log the value of i. i is just passed as function definition.

- Then arr is returned, gets saved in f.

- As build finishes executing, the value of i increments to 3, and all function definitions have been returned.

- build() is cleared from the execution stack.

- f has all the 3 functions.

	```
	f[0]();
	f[1]();
	f[2]();
	```
	
- Each of these functions called needs to access the value of i.

- But execution stack of build has finished executing and is no longer there.

- Yet, the final value of i is retained in the global scope. 

- The variable environment of build is preserved due to closure.

- Thus, all 3 functions print 3, which was the final value of i.

- If you wanted to print 1,2,3, use let i. let datatype segments the memory.
It stores each new value of i in the for loop in a different memory location.

- IIFE is another way to have 1,2,3 printed. Just enclose the return function statement inside an IIFE
Pass the counter to the IIFE and refer to that variable inside the actual function definition to be returned.
For each iteration of the loop, a new execution context for each IIFE will be created, thus referencing the correct values of the counter.

This is very similar to getting closure after watching Star Wars series.
The episodes you are yet to watch, are functions authorized to access the part of your neural network.
As the story progresses, the information in your brain is updated.
When you finish watching episode 3, you get closure. 
You are no longer desperate or curious.
The first series is gone, has finished, and yet you retain the information, the latest version of it.
And this information flows through the next trilogy even after the first one is over.
The first trilogy is gone, yet the second one can access it. 
Because the information is retained in your brain.

## Call, apply and bind

Every function has:
- name property
- code property which is invokable
- and

- call
- apply
- bind

All 3 have to do with `this` variable

**bind** creates a `copy of the function` and sets `this` of the function to the first parameter passed.

**call** calls the function while altering its `this`
 
- call executes the function and bind creates a copy

**apply** requires an array of arguments passed to it. It works just like call but needs an array of arguments.

### Function borrowing (call, apply)
Invoke the original function present in first object and _apply()_ a second object to it to display the second person’s name. It tricks the `this` inside the original function into thinking that it belongs to the second object.

	> var Person = {a:"a", b:"b", func: function(){console.log(this.a)}}
	< undefined
	> var dog = {a:"Doggo"}
	< undefined
	> Person.func.call(dog)
	[Log] Doggo

### Function currying (bind)
- Creating a copy of a function with some preset parameters.

Passing a second parameter (say 2) to bind sets the first argument of the original function to a permanent value of 2
However, when you call the new function, the first parameter will always be 2.
Any argument passed to the new function will apply to the second parameter(and not the first because it is preset), and so on.

	function mult(a,b){return a*b}
	var x2 = mult.bind(this,2); //This sets x2's a to 2 permanently
	x2(3); returns 6
	
Note how mult takes 2 parameters but x2 takes only one. That's because we curried the first parameter of x2 to a 2.

# HTTP Basics

## HTTP

- Used for communication between computers
- Connectionless:
	Browser initiates request then disconnects.
	Server finds a route and sends data.

- Media independent: Any type of data is welcome

- Stateless: Client & server are aware of each other only during current transaction. 
	Then they forget about each other.
	Neither client or server retains info.

## Client
Sends request to server in the form of a request method + protocol+ MIME like message and maybe some body content over TCP/IP

## Server
responds with status line, protocol+success/error code+MIME like message

## MIME
a standard for formatting files of different types, such as text, graphics, or audio, which can be played by a web browser or email application.

`HTTP/1.0` - protocol version
`HTTP://host:port_no/path` - URI

All date time in GMT

Charset is ASCII

encoding: encoding algo to encode data before passing

Media type example: image/gif

lang: en-US

## HTTP Methods
- GET - only get data 
- POST - send data
- PUT - Replaces info with new
- DELETE
- CONNECT - tunnel to server
- OPTION - get possible actions

## req/resp structure

- status line
- 0* headers
- empty line
- optional message body

## Status code
- 1xx - Info
- 2xx - Success
- 3xx - Redirect
- 4xx - Client error
- 5xx - Server Error
