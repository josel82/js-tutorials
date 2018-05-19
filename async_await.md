## Async/Await

Is a better still way (at least from my point of view) for dealing with asynchronous code. In order to understand Async/Await it is necessary that you understand Promises first. If you don't understand Promises I recommend you read my tutorial on [Promises](promises.md), maybe you want to visit [Mozilla Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) or if you prefer you can watch [this video](https://www.youtube.com/watch?v=2d7s3spWAzo).   

If you are still reading this, I will assume that you understand Promises, or at least have an idea of how they work. As we know, the whole purpose of using Promises is that of writing cleaner and more maintainable asynchronous code. However, Promises can still get a bit messy some times. Let me show you what I mean by that with in following example.

source code from: https://javascript.info/promise-chaining
```JavaScript


       // Make a request for user.json
      fetch('/article/promise-chaining/user.json')
        // Load it as json
        .then(response => response.json())
        // Make a request to github
        .then(user => fetch(`https://api.github.com/users/${user.name}`))
        // Load the response as json
        .then(response => response.json())
        // Show the avatar image (githubUser.avatar_url) for 3 seconds (maybe animate it)
        .then(githubUser => {
          let img = document.createElement('img');
          img.src = githubUser.avatar_url;
          img.className = "promise-avatar-example";
          document.body.append(img);
      
          setTimeout(() => img.remove(), 3000); // (*)
        });
        
```

Here we have a nice example of promise chaining. We start by calling fetch which returns a promise, therefore we can use 'then', within which we get a response once the promise is resolved. Then we return response.json() which in turn returns a promise, thus we can use then again in order to wait on it. Inside that 'then' we are expecting a user which we use as a parameter for making another http request using the fetch function and we return it, we know that fetch returns a promise right, so that allows us to use 'then' once more. Inside that 'then' we expect a response, then we return response.json() which returns another promise, thus I can use then yet one more time. Finally, we get the data we were looking for and use it to do cool stuff on the browser. 

I hope you have got that, and if you didn't that's totally fine. That code can be a little bit tricky to understand. Let me show how that code looks using Async/Await


```JavaScript


      const fetchUser  = async(){
      
          const response   = await fetch('/article/promise-chaining/user.json'); 
          const user       = await response.json();// Load it as json
          const response2  = await fetch(`https://api.github.com/users/${user.name}`);// Make a request to github
          const githubUser = await response2.json();// Load the response as json
          
          // Show the avatar image (githubUser.avatar_url) for 3 seconds (maybe animate it)  
          let img = document.createElement('img');
          img.src = githubUser.avatar_url;
          img.className = "promise-avatar-example";
          document.body.append(img);
          
          setTimeout(() => img.remove(), 3000); // (*)
          
      }
      
        
```
I don't know about you, but I think this code is way more easier to understand. And it is so because it reads as synchronous code. As this example illustrates, Async/Await allows us to write asynchronous code that reads as synchronous code. It works like this: the await keyword, when placed before a __Promise__ (this only works with Promises), tells JavaScript to stop and sit on that line, waiting until the promise is resolved. Once the promise is resolved, it returns the resolved value of the promise which we can then assign to a variable and use it like we did in the example. "That's ok, but how about the 'async' keyword??" Well, in order to be able to use the 'await' keyword inside a function, we need to place the 'async' keyword just before that function. It is kind of like a mark that indicates that we are allowed to use the await keyword inside that function. Got it?

## Error Handling

"Ok Jose, you told me that Promises can reject, what happens in that case?? how do we handle this cases??" 
Patience young grasshoper... here is how you do that:

```JavaScript


      const fetchUser  = async(){
          const user = {
            id: 23,
            name: 'Lisa',
            lastname: 'Simpson'
          }
          
          try{
            const response2  = await fetch(`https://api.github.com/users/${user.name}`);// Make a request
            // we do cool stuff with the response
          }catch(error){
            // if something goes wrong the error is caught 
            console.log(error) // and handled
          }
         
          
      }
      
        
```
You can wrap the promise within a try/catch and problem solved...


I hope this has help you understand Async/Await. If not you can leave a comment or get more information on [Mozilla Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) or by watching [this video](https://www.youtube.com/watch?v=568g8hxJJp4&t=1090s)
