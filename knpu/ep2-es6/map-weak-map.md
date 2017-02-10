# Map Weak Map

So far, everything thing we've talked about have been new language constructs, like the let and const keyword, the class structure, and the template strengths. That's not on accident. That's the hardest stuff to understand about ECMAScript 2015, but there's also a lot of other stuff. Like new functions and new objects. Now, for the most part, those are easy to understand. If you see a new object or function that you've never seen before, you can look it up, see how it works, and you're good to go. However, there is one set of objects, no pun intended as you'll see, that I do want to talk about. The first one is called a Map. First, let's go into our play.js.

Let's look at how we previously would create an associative array, or a ... hash, which is also an object in JavaScript. We would say foods equals open curly, close curly, and then we could start adding a bunch of keyeds to it, like foods.Italian, foods.Mexican ... and foods.Canadian maybe. Of course, at the bottom we'd say foods.Italian to print out that key. No surprise, that works perfectly. In ECMAScript 2015, we now have the option, instead of creating a simple object, to create a new Map object. Now, the syntax for this is slightly different. Instead of foods.Italian, it's foods.set Italian. You pass the item as the second argument. Other than that, you can see that we're effectively doing the same thing that we did before. Of course at the bottom, we're gonna do the same thing. Say, foods.get Italian. Low and behold, that works nicely.

Okay, so we have a new Map object and it's a different way to create an associative array. Why would we use this? Well, the biggest reason is that it has more helpful methods on it. For example, we can say foods.has French, and that just returns false. It wasn't difficult to do before with objects, but it has this nice, fluid interface that's very easy to use. It has a number of other methods on it, as well. Like contains, which will be a way for you to see if an element is contained inside of that Map. It has one other super-power, which is kinda crazy, and that is ... non-string keys.

For example, let's create a new variable called let southern US states. We'll set this to an array. Tennessee, Kentucky, and Texas. Now, we can actually say foods.set southern US states, and set that to hot chicken. In this case, this is actually an object. It's an array, but it's okay for us to use it as a key. By the way, hot chicken is really only something you should eat in Tennessee, but for an example, I needed to include the other states. Down here we do foods.get southern US states and that's gonna work the same way as before. Okay, so that's kinda cool. More complex keys, and this is actually gonna come in handy in a second. As far as a useful thing you can do with it, another one that's very useful is just foods.size. That's gonna print out four. That is the Map.

There are more methods you can call in it and you should look into those, but it's fairly simple. There's something else called a WeakMap. This is where things get a little bit interesting. Why do we have a Map and a WeakMap? What's the difference? Well, first let's try to run this and see what happens. Actually you can see that it fails. It says invalid value used as WeakMap key. At first, Map and WeakMap are basically the same, except WeakMap seems to be a worse version of Map because one of its requirements is that its keys must be objects. So, I'm gonna turn each of the these into a raise, which are objects in JavaScript, because the WeakMap is gonna force me to do that. When I get, I will get the Italian. Now when I run it, it works fine. Or, does it?

Two interesting things. Notice I have undefined hot chicken undefined. First, even though this array is equal to this array up here, they are not the same object in memory. Those are two distinct objects, so they're not identical. So, it's not going to see them as the exact same key. Second, the WeakMap, you can't actually call foods.size. That's not something that works with the WeakMap. I'm gonna show you one other crazy thing, which really starts to show you the purpose of the WeakMap. After we set the southern US states onto the array, I'm gonna say southern US states equals null. Now, a second ago, this was printing hot chicken. Now, it actually prints undefined. So, the purpose of the WeakMap, and we will see an example in a second, the different between a WeakMap and a map ... is garbage collection.

If the WeakMap in JavaScript, if you have a variable that isn't referenced by anything else anymore, then garbage collection removes it from memory. When you put things inside of a WeakMap, that doesn't prevent garbage collection. So, even though southern US states is still on our WeakMap, since it's not being referenced anywhere else, it gets removed via garbage collection. The question is, why the heck would we ever use the WeakMap? Because at this point, I'm thinking the Map is nice and I'm gonna use the Map all over the place. I'm never, ever, ever gonna use the WeakMap. Well, I'm gonna show you a use case to the WeakMap. You may or may not use this use case, but at least you'll recognize what's going on.