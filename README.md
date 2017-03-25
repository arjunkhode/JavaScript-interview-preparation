# JavaScript-interview-preparation
My preparation for getting a full time job as a front end developer
______________________

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
