# JavaScript-interview-preparation
My preparation for getting a full time job as a front end developer

* The null gotcha!

  null datatype qualifies as an Object.
  ```
  const bar = null;
  console.log(typeof bar === "object"); //returns true!
  ```

  If you want to reliably check if bar is an object, check for null condition first.
  ```
  console.log((bar !== null)&&(typeof bar === "object"));
  ```

  1. If bar is a function, the above code will return false.
  If you want to return true for bar being a function, simply add the following with an and condition
  ```
  (typeof bar === "function")
  ```
  
  2. Arrays are Objects too, so the expression will return true for arrays. 
  To return false for arrays, use the toString.class() method:
  ```
  (toString.call(bar) !== "[object Array]"))
  ```
 
* Since toString is defined in Object.prototype, whoever inherits Object, will by default get the toString method.

  But, Array objects, override the default toString method to print the array elements as comma separated string.
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
  
  b would be accessible and defined outside the function, but a would not be defined in the global scope because it has a var prefix in the declaration
  
  If the statement had const instead of var, neither of the variables would print outside the block's scope

* Coercion

  Type coercion means that when the operands of an operator are different types, one of them will be converted to an "equivalent" value of the other operand's type. For instance, if you do:

  ```
  boolean == integer
  ```
  the boolean operand will be converted to an integer: false becomes 0, true becomes 1. Then the two values are compared.

  However, if you use the non-converting comparison operator ===, no such conversion occurs. When the operands are of different types, this operator returns false, and only compares the values when they're of the same type.
  [source](http://stackoverflow.com/questions/19915688/what-exactly-is-type-coercion-in-javascript)
