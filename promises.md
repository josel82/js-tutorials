## Promises

A __Promise__ is an object that _represents the eventual completion (or failure) of an asynchronous operation, and its resulting value_ (fscholz, 2018).

In simpler words, let's say that Promises are a better way for dealing with asynchronous code. Before Promises, we only had callbacks, and they were fine until applications got bigger and more complex and developers started to come across problems like this:


![callback hell](img/callback_hell.jpeg "Callback Hell")

Behold the __Callback Hell__!

At the beginning Promises were just an implementation with the purpose of overcoming problems like these, but they became so popular that they ended up added to JavaScript in 2015.

## How to create a promise

To create a promise all we need to do is to call its constructor, as shown on the sample below.
This constructor takes in an anonymous function which has two parameters: __resolve__ & __reject__, and returns a pending promise which is then assigned to the variable 'myPromise'.

Inside this function that we pass inside the constructor is where we write the instructions for how that Promise will be fulfilled. After some asynchronous task has been performed, we call __resolve__ in the successful case, or we call __reject__ in case something goes wrong.
Bear in mind that a Promise either resolves or it gets rejected, or is in a pending state. 
(A pending Promise is a promise that hasn't been resolved or rejected).
```JavaScript

  const myPromise = new Promise((resolve, reject)=>{
    
      setTimeout(()=>{ //simulates an asynchronous task
      
        resolve('Hello from myPromise'); //resolves the promise. 
        
      },3000);
      
  });
  
  console.log(myPromise); //Outputs: Promise { <pending> }
  
  
```

Notice in the example above we are getting a pending Promise when we print it to the console. Why is that? 
Well, that is because by the time we console.log 'myPromise', this still hasn't been resolved. As I explain in my tutorial on [Callbacks](callbacks.md), the way the JavaScript engine handles asynchronous code is, it puts it aside until that task is done, meanwhile the JavaScript engine continues running the next lines of code. 

Now, how can we run some code when the promise is resolved?

## then()

Promises provide a method called 'then', this method gives us access to any data passed in the resolve callback and it runs any code you put inside when the promise is resolved. see the code below.

```JavaScript

  const myPromise = new Promise((resolve, reject)=>{
    
      setTimeout(()=>{ //simulates an asynchronous task
      
        resolve('Hello from myPromise'); //resolves the promise. 
        
      },3000);
      
  });
  
  myPromise.then((data)=>{ // this anonymous function we are passing into the 'then' function is the resolve callback we call from inside the Promise and the parameter 'data' has the value we passed in, in this case ('Hello from my Promise') 
  
      console.log(data); //Outputs: Hello from myPromise    (after 3 seconds)
      
  })
  
  
```
Using the same example, see how this time instead of getting a pending promise, we get the string we passed in the resolve callback after 3 seconds (when the promise resolved). 

So far so good, now let’s see how we reject a Promise. To reject a promise all we have to do is to call the reject callback from inside the promise. There's one thing though, we can't use the then function in order to run code when the Promise gets rejected, for that ne have to use the 'catch' function instead.

```JavaScript

  const myPromise = new Promise((resolve, reject)=>{
    
      setTimeout(()=>{ //simulates an asynchronous task
      
        reject('Ups! Something went wrong'); //resolves the promise. 
        
      },3000);
      
  });
  
  myPromise.then((data)=>{  
  
      console.log(data); //This code will never run
      
  }).catch((error)=>{// this anonymous function we are passing into the 'catch' function is the reject callback we call from inside the Promise and the parameter 'error' has the value we passed in, in this case ('Ups! Something went wrong')
  
      console.log(error); //Outputs: Ups! Something went wrong    (after 3 seconds)
      
  });
  
  
```

## catch()

We use the catch function for handling promise rejection. This function gives us access to the data we pass through the reject callback and allows us to run code when the promise is rejected.


Nice! Let's now add some uncertainty to this example, by either resolving or rejecting the Promise depending on a condition. This Promise will resolve if the value of 'random' is greater or equal than 0.5, otherwise it will be rejected.

```JavaScript

  const myPromise = new Promise((resolve, reject)=>{
    
      let random = Math.random();
      
      setTimeout(()=>{ //simulates an asynchronous task
      
        if(random >= 0.5){
            resolve('Resolved with value: '+random);
        }else{
            reject('Rejected with value: '+random);
        }
        
      },3000);
      
  });
  
  myPromise.then((data)=>{  
  
      console.log(data); //runs if random >= 0.5
      
  }).catch((error)=>{
  
      console.log(error); //runs if random < 0.5
      
  });
  
  
```

## Real life example

"Ok ok, enough of easy examples, show me the real stuff!"
You got it! This one is courtesy of the [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)  

Here we are calling the fetch method, to which we are passing a url, and an options object which contains metadata used for setting the HTTP request. The fetch method returns a __Promise__. That's why you see both the then & catch methods chained at the end. These as we saw are for responding to either a successful or an unsuccessful response.

```JavaScript

  var url = 'https://example.com/profile';
  var data = {username: 'example'};
  
  fetch(url, {
                method: 'POST',
                body: JSON.stringify(data), // data can be `string` or {object}!
                headers: new Headers({
                  'Content-Type': 'application/json'
                })
              }).then(res => res.json())
                .catch(error => console.error('Error:', error));
                
```

Here is another way to see it. It does exactly the same it is only expressed slightly different for illustration purposes.
```JavaScript

  var url = 'https://example.com/profile';
  var data = {username: 'example'};
  
  const pendingPromise = fetch(url, {
                            method: 'POST',
                            body: JSON.stringify(data), // data can be `string` or {object}!
                            headers: new Headers({
                              'Content-Type': 'application/json'
                            })
                          });
  
  
  pendingPromise.then((res) => {
      res.json() // runs in case of a successful response
  }).catch((error) => {
      console.error('Error:', error); // runs in case of a bad response
  });
                
```

I know Promises can be a bit difficult to understand at first. And if you didn't understand that's totally fine. I didn't understand Promises the first time I saw them. As a matter of fact, it took me quite a while to really understand how they work and feel comfortable using them. 

If you want to dig more into Promises visit [Mozilla web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
or watch [this video](https://www.youtube.com/watch?v=2d7s3spWAzo), this guy is really good at explaining these concepts.


