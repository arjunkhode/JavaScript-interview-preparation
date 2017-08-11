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

- In case of DOM event handler, value of this will be the DOM element. Like if you have an addEventListener that types this. It will be `<element>`.

https://www.youtube.com/watch?v=yuo8YqKDQ-M

# Callback functions

- A function passed as an argument to another function is a callback function.

- Callback functions are not immediately executed. They are just passed as parameters and the parent function decides when to execute the callback.

- Callback functions are closures. 

# Arrays

- Array.concat() is 40% faster than Array.push

- Array.unshift() adds elements to the starting of the array

- Array.push() modifies the original array. Array.concat() returns a new array.

- * Array.concat() copies object references instead of values

- To concatenate arrays, Array.push() is sometimes faster than spread. 

```
let arr1 = [1,2];
let arr2 = [x,y];
arr1.push.apply(arr1,arr2);
// Note: arr1.push(arr2) would push an array inside array
```

- Removing duplicates from an array using filter

- Filter callback returns a boolean, and based on that adds elem to the resulting array.

```
arr.filter((elem,i,arr)=>{
	return arr.indexOf(elem)===i;
});
```

- Reduce uses prevVal and elem. It also requires an initial value to initialize prevVal with.

arr.reduce((prevVal, elem)=>{return prevVal+elem;},0);

- Arrays are passed by reference

- *To pass an array by value, use Array.slice()
- In short, it doesn't work for objects, but works for strings and numbers.

- For object references(variables) slice copies the objects into a new array. But modifying the original object modifies the values of the slice array
- For numbers and strings, slice passes them by value. So modifying the original array does not change the slice array.

- In Splice, NaN is treated as 0 so arr.splice(NaN,4) will delete 4 elements from arr[0]

- To sort numerical values, use the following
```
var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a-b})
```

- undefined is not false
- null is not false
- undefined is null
- null is not 0
- undefined is not 0
- escape sequences are equal to empty string

# Currying

```
function greetcurry(greeting){
	return function(name){console.log(greeting,name);}
}

>const hellogreeting = greetcurry("Hello");
>hellogreeting("Arjun");
>Hello Arjun

// first paren returns a function that greets hi
// call that function with parameter Arjun
>greetcurry("Hi")("Arjun");
```

# DOM

- no element returns null
- document.body.children gives all child elements

```
HTMLCollection (10) = $2
0 
<div class="position-relative js-header-wrapper ">…</div>
1 
<div id="start-of-content" class="show-on-focus"></div>
2 
<div id="js-flash-container"> </div>
...
```
- document.body.childNodes gives all childNodes

```
NodeList (21) = $1
0 #text " "
1 
<div class="position-relative js-header-wrapper ">…</div>
2 #text " "
3 
<div id="start-of-content" class="show-on-focus"></div>
4 #text " "
5 
<div id="js-flash-container"> </div>
...
```

- firstElementChild
- lastElementChild
- previousElementSibling
- nextElementSibling
- tagName is an uppercase name of element
- `document.body.innerHTML+="<div>Wasaniga</div>"` this works. But innerHTML can't be appended. It acts like it is immutable.


### Attributes

- elem.hasAttribute(name)
- elem.getAttribute(name) gets the value of that attribute
- elem.setAttribute(name, value)
- elem.removeAttribute(name)
- Attributes are not case sensitive
- input.checked // true or false
- input.getAttribute('checked') // returns string of content (not boolean)

### DOM Modification

- document.body.appendChild(textElem); // Always need parent element to call this function
- elem.insertBefore(newElem, targetBeforeWhichToInsert);
- removeChild(elem);
- custom insertAfter function
```
let elem = document.createElement('div');
elem.innerHTML = "Hi! I'm the new element!";
function insertAfter(elem, target){
	return elem.parentNode.insertBefore(elem, target.nextSibling);
}
// usage
insertAfter(elem, document.body.firstChild);
```

## Bubbling and capturing

- event.stopPropagation();
- If there are two onclick handlers on the same link, then stopping bubbling in one of them has no effect on the other one.
- Using addEventListener with last argument true is only the way to catch the event at capturing.
- `elem.addEventListener( type, handler, phase );`

### The default browser action

// 1) Event special method event.preventDefault() for W3C-compliant browsers and event.returnValue = false for IE<9.
// Or, in a single line:
event.preventDefault ? event.preventDefault() : (event.returnValue = false);

// 2) Return false from the handler

```
element.onclick = function (event) {
  return false;
};
```

- event.preventDefault()

- You have to bind the `this` inside a click or other event because by default, the `this` will point to the element that activated the event. So if you want to use any data/function from a structure outside the scope (other than DOM), you bind that object inside the click callback.

- Numbers in JS are represented as a whole number times a power of 2. This makes values with denominator 10 inaccurate.

- Avoid using for...in loop to iterate over arrays. It traverses the structure in arbitrary order.

- *Object.hasOwnProperty(prop) returns a boolean check whether object has that property

- By definition, null has no prototype, and acts as the final link in this prototype chain.

#### Constructors vs Object literals

- Constructors also allow another level of flexibility since functions provide closures, while object literals do not.

- Constructors are meant for many instances. Objects are one off.

- Constructors make a new context and set `this` to the context. Object literals have the outer scope assigned to `this` but don't have an outer execution context, just lexical scope.

```
// Constructor 

> class Dog{constructor(){console.log(this)}}
> let d1 = new Dog
[Log] Dog {}

// object

> let cat = {print: function(){console.log(this)}}
> cat.print()
[Log] {print: function}
< undefined
```

### Logical operations on strings

for &&, the last valid value is returned
for ||, the first valid value is returned

```
  var a = true;
  var b = 'Yes';
  var c = 'It\'s me';

  console.log(a && b);  // Prints 'Yes'
  console.log(a && b && c); // Prints 'It's me'
  console.log(a && b || c); // Prints 'Yes'
```
