## Callbacks

Callbacks are functions which other functions call after they are done with some asynchronous task. Got that? not quite, right? Let's see if I can make this easy for you.


In order to understand callbacks we need to first understand what __Higher Order Functions__ are. Higher order functions are a really cool feature in JavaScript. Basically they are functions which take in another function as an argument. "Ok, stop talking, and show me some code!!" 

```JavaScript
  
  // do stuff takes a function as an argument. Therefore, it is a higher order function
  function doStuff(fn){   
      fn(); // calls the function
  }
  
  function doMoreStuff(){ 
      console.log('I do cool stuff');
  }
  
  doStuff(doMoreStuff);  //Outputs: I do cool stuff
  
  
```
Now, have a look at the code bellow. This is equivalent to the code above. We have just expressed it slightly different. Instead of declaring 'doMoreStuff' as we did before,  we are passing the exact same function as an anonymous function (an anonymous function it's just a function which doesn't have a name)

```JavaScript
  
  // do stuff takes a function as an argument. Therefore, it is a higher order function
  function doStuff(fn){   
     fn(); // calls the function
  }
  
  doStuff(function(){ 
       console.log('I do cool stuff');
  }); 
  
  
```
The following piece of code, once again does the same thing. But in this case, we are just using ES6 syntax, because... because we are awesome.

```JavaScript
  
  // do stuff takes a function as an argument. Therefore, it is a higher order function
  const doStuff = fn => fn();
  
  doStuff(() => console.log('I do cool stuff')); 
  
  
```

Now, stop for a second and try to think about what we have done here. We have declared a __Higher order function__ 'doStuff' to which we have passed in another function as an argument, which we have called-__BACK__ from inside 'doStuff'... &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;got it???

"Wait a second", you may say. "What’s the point of doing all that work around to perform a task that we could just as well have run from inside 'doStuff'???" 
You are right, in this example that just doesn't make sense, but that was just an example right? I just used it to explain what higher order functions are and what a callback is.

Now let me show you what Callbacks are useful for.

Let's imagine our old friend Damo is walking around Dublin, on a lovely rainy day, and he wants to smoke a cigarette. He searches in his pocket just to find out that he ran out of 'smokes'. Bad luck, but that won't keep him from enjoying a 'loovely' cigarette. He goes and starts to ask other people for a cigarette. Since it will take some time until someone gives him a cigarette, we can say that this is an asynchronous task.

So, it doesn't take too long until Damo gets a cigarette. Now he can go and smoke it, just to find out that it wasn't exactly tobacco what they gave to him... 'Oh Jaysus'. 

Let's try to replicate this in the code bellow. Here we declare a function 'getSmokes'. Inside we have placed a setTimeout to simulate the time it would take Damo to get a cigarette. We set the delay to 3000 and call the callback function once that time has passed (once he finds smokes).

Then we declare the callback function, which in our example is the 'smoke' function. Finally, we call 'getSmokes' passing 'smoke' as an argument as shown below. Got that??

```JavaScript


  function getSmokes(callback){
    // go ask for smokes. this will take some time (3 secs to be precise)
    setTimeout(()=>{
         callback('not exactly tobacco')// once it finds some smokes it calls the callback
    },3000);
  }
  
  function smoke(type){
    console.log('Smoking '+type);
  }

  getSmokes(smoke); // Outputs: Smoking not exactly tobacco    after 3 seconds
  
  
```

Again, here is another way to express the same case. In this case, instead of declaring the 'smoke' function like we did before, we pass it into 'getSmokes' directly as an anonymous function.

```JavaScript


  function getSmokes(callback){
    // go ask for smokes. this will take some time (3 secs to be precise)
    setTimeout(()=>{
         callback('not exactly tobacco')// once it finds some smokes it calls the callback
    },3000);
  }
  

  getSmokes(function(type){
  
    console.log('Smoking '+type);
    
  }); // Outputs: Smoking not exactly tobacco    (after 3 seconds)
  
  
```

### Why do we need callbacks???
JavaScript is a non-blocking I/O programming language. This means that instead of waiting until a task is done in order to do the next task, the JavaScript engine puts those asynchronous tasks aside and continues with the other tasks. Once the asynchronous task is done, the JavaScript engine puts it back to the 'execution line'.

Going back to the previous example, our friend Damo will be signing while he is getting smokes. "But How come? if we are printing after we have called the getSmoke function!" Well, that is because 'getSmoke' has some asynchronous code which the JavaScript engine is putting aside until is completed, then continues on printing 'Singing in the rain...' on the console, and it is not until 3 seconds have passed that this task is done that we get 'Smoking not exactly tobacco' printed on the console. 

So what the callback is doing here, it is allowing us to run code when this asynchronous tasks is done, and that code is the code we have written inside the callback function.

```JavaScript


  function getSmokes(callback){
    // go ask for smokes. this will take some time (3 secs to be precise)
    setTimeout(()=>{
         callback('not exactly tobacco')// once it finds some smokes it calls the callback
    },3000);
  }
  

  getSmokes(function(type){              // called first
    console.log('Smoking '+type);
  }); 
  
  console.log('Singing in the rain...'); // called second
  
  
  // Output: 
  // Singing in the rain
  // Smoking not exactly tobacco    (after 3 seconds)
  
```

For more information go to [this page](https://www.w3schools.com/jquery/jquery_callback.asp)
or you can watch [this video](https://www.youtube.com/watch?v=BMUiFMZr7vk)
