## Closures
---

As defined by Mozilla, _a closure is the combination of a function and the lexical environment within which that function was declared_.  

```javaScript
  
  
  let name = 'Damo' 
  // Outter scope
  
  function sayHello(){ 
    // Inner scope
    console.log('Alright '+name+'!'); 
  }
  
  sayHello(); // Outputs: Alright Damo!
  
```

In the example above, we have a function, which uses a variable that has been declared in its outer scope (Outside of the function). The fact of using this variable (that is outside of itself) makes this function a closure, and that is because this function has a reference to that variable (outside), which access when gets called, like in the example.

It is important to understand that a closure does not store the value of these variable, it only stores a reference of such variable. This implies that if we were to change the value of the variable __name__ before calling __sayHello__ it would be reflected in the output. see the example bellow:

```javaScript
  
  
  let name = 'Damo' 
  // global scope
  
  function sayHello(){ 
    // local scope
    console.log('Alright '+name+'!'); 
  }
  
  name = 'Ivor'
  
  sayHello(); // Outputs: Alright Ivor!
  
```

Now, lets look at another example. Here we have a nested function 'defineSize' that uses a parameter 'species' of the outer function. Now, if we remember the definition of a closure, we will see that 'defineSize' is a closure, because it is using a parameter of the outer function (which is part of its lexical environment).


```javaScript
  
  
  // global scope
  function createAnimal(species){ // species is a parameter of 'createAnimal'
    // outer function scope 
    return function defineSize(size){
    // local scope of 'defineSize'
      console.log('I am a '+size+' '+species);
    }; 
  }
  
  const dog = createAnimal('dog'); // returns closure 'defineSize', which contains a reference to 'species'
  dog('big'); // Outputs: I am a big dog
  
  
```
When we call 'createAnimal', it returns the 'defineSize' closure, which we then store in the variable 'dog', meaning that now the variable dog, contains a reference to the 'defineSize' closure.
As we have seen before, closures hold a reference of the lexical environment they are declare in. Since when we called 'createAnimal' we passed in the string 'dog' as an argument, this value is now being held inside the closure 'defineSize', so when we call the closure, passing the string 'big', we get 'I am a big dog' printed to the console as shown in the example.


Notice that closures have three types: of scope. 
* __Global scope:__ The highest scope level. Variables that are declared outside of a function are global. These variables are visible within all the functions.
* __Outer Functions scope:__ the scope of the function within which the closure is declared in. closures have access to any variable or parameter within the scope of its parent function.
* __Local scope:__ variables declared within the closure are in the local scope.

For more information about closures: [Click Here!](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
I also recommend watching this video: [Closures - Part 5 of Functional Programming in JavaScript](https://www.youtube.com/watch?v=CQqwU2Ixu-U)

