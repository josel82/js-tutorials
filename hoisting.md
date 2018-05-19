## Hoisting

It is JavaScript's default behaviour of moving all variable declarations to the top of the current scope (the top of the script or the top of a function).

Example:
```JavaScript


  function printSomething(){
      x = 'Something';
      console.log(x);
      const x; 
  }
  //Same as
   function printSomething(){
      const x; 
      x = 'Something';
      console.log(x);
  }
  
```
In the case above, the JavaScript interpreter moves the declaration of the variable "x" to the top of the scope, which in this case is the function "printSomething", by default. (If you don't understand how scope works in JavaScript, you can find some info about it in my tutorial on Closures or in this [page](https://www.w3schools.com/js/js_scope.asp))

Now, let’s imagine we didn't declare the variable "x" within the function. In this case the JavaScript interpreter will go up one level in scope and check if the declaration is there. It will do so until either finds the declaration or it reaches the global scope, where it will declare the variable in case it hasn't been declared. 


```JavaScript


  var x;
  
  function printSomething(){
      x = 'Something'; //The JavaScript interpreter will declare this variable in the global scope if we don't declare it inside the function.
      console.log(x);
  }
```

## var, let, const
__var__ is the key word we used to use for declaring variables in ECMAScript5. __var__ has function scope, meaning that its scope is determined by the function it has been declared in. See the example below.

```JavaScript


  var x;
  
  function myFunction(){
     
     var myLocalVariable = "Some value"
     
     console.log(myLocalVariable) // prints: "Some value"
  }
  
  console.log(myLocalVariable) // prints: undefined
  
```
This example illustrated the definition of the scope of a variable. The variable is only accessible inside of the function it has been declared in. Now, let’s see what happens when we place it inside of a loop:

```JavaScript


   for(var i = 0; i<=10; i++){
      console.log("inside loop: "+ i) 
      // prints: 
      // inside loop: 1
      // inside loop: 2
      // inside loop: 3
      // ...
      // inside loop: 10
   }
    console.log("outside loop: "+ i) 
      // prints: 
      // outside loop: 1
      // outside loop: 2
      // outside loop: 3
      // ...
      // outside loop: 10
 
```
As shown in the example above, the variable is available outside the loop. This is because variables declared with the __var__ keyword are function scoped, and a loop is not a function, therefore it is available outside of it as well. This is not the case with the __let__ and __const__ keywords, introduced in ECMAScript6. Variables declared with those keywords would stay within the scope of a loop. see the example bellow:

```JavaScript


   for(let i = 0; i<=10; i++){
      console.log("inside loop: "+ i) 
      // prints: 
      // inside loop: 1
      // inside loop: 2
      // inside loop: 3
      // ...
      // inside loop: 10
   }
    console.log("outside loop: "+ i) 
      // prints: undefined
      
```
It is for this reason that it is recommended the used of __let__ and __const__ over __var__.
The main difference between __let__ and __const__ is that the value of a variable using let can be changed whereas a variable using const can't change its value. 

```JavaScript


   let x = 3;
   x = 6; // allowed
   
   const y = 9;
   y = 40; // not allowed
      
```

