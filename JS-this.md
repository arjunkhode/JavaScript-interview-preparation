- NaN is type Number
- null is an object
- call calls the function replacing its this. Apply is like call
- bind creates a copy of the function without executing it. 
- toString.call(variable) === [object Array];
-  Array.slice(starting index, index before which to stop);
- With a negative starting index, 'slice' offsets the array from the end by that magnitude
- Use strict does not allow variables or 'this' to default to global
- []+5 equals "5"
- lexical scope means where the function physically resides in the code
- A function used as getter or setter has its this bound to the object from which the property is being set or gotten.
- In arrow functions, this is set lexically, i.e. it's set to the value of the enclosing execution context's this
- Outer variable environment lexically placed is called scope chain
- An IIFE creates a new execution context and stores all its variables inside safely. It never overwrites the global variable of the same name.
- Objects are passed by reference, any operations mutate the object. But = operations never mutate the reference, it is an assignment. 
- Array.indexOf() is type and instance sensitive. You need to pass objects as variables and not as definitions to indexOf for it to find it.
- indexOf() can accept a second parameter that tells it to find parameter 1's instance AFTER the second parameter is placed in the array.
- Slice never changes original array
- Splice has 3 parameters
	1. index
	2. number of elements to delete
	3. stuff to replace the deleted elements with
- Always use Splice to delete elements. Not delete arr[3], which creates a hole in arr[3] and doesn't change the length of the array. 
- Built in Boolean function as filter
["happy","new","", 0 ,"year",false].filter(Boolean)
returns ["happy","new","year"]
- Array.isArray([]); // To check if array (object is not array)

# Closure
 
 If there is a function that relies on an outer variable which is part of another outer function.

 Even when the outer function has finished executing
 and has popped off the stack, the inner function can still access the variable value. It is like a snapshot of that variable.

```
 function a(){
 	var x = 5;
 	function b(){
 		console.log(x);
 	}
 	return b;
 }
```

 let c = a(); // function a has ran fully
 c(); // b is stored in c and is executed
 > 5  // by now, x should have disappeared but it hasn't
 //objects are passed by reference. So b's x is still in c's x

 - Another example
```
 function p(){
 	var arr = [];
 	for(var i=0; i<3; i++){
 		arr.push(function(){console.log(i)})
 	}
 	return arr;
 }

 let q = p(); // p is popped off stack
 q[0]();
 q[1]();
 q[2](); // All return 3, the last value of i
```
# This of an object

function inside object has its this set to object

# This of a function

- function is also an object. We can set properties to a function.

function fun(){//something};
fun.cool = "true";

- *** this of a function exists only during execution time ***

fun.this 
returns undefined

- If it is IIFE, this will be window

- If use strict on IIFE, this will be undefined

# DOM event handler

- In case of DOM event handler, value of this will be the DOM element. Like if you have an addEventListener that types this. It will be '<element>'.

https://www.youtube.com/watch?v=yuo8YqKDQ-M


