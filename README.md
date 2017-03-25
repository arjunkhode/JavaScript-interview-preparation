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

  
