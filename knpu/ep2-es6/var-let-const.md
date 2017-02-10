# Var Let Const

One of the most noticeable changes you're going to see with ECMAScript 2015 JavaScript is suddenly, instead of seeing var everywhere, you're going to see let everywhere. For example, scroll all the way down to the bottom, and you can even see that PhpStorm highlights var and says, "var used instead of let or const," and we'll talk about both let and const. Even PhpStorm is sort of telling us, hey, you should maybe use let instead of var. Now var is not going away, but let's find out what is going on with this let. Let's change var to let and down here, let's console.log(totalWeight). I'm going to go back over here and refresh. This function is called a bunch of times as the table is being loaded, so you can see it totaling up each time. It appears that everything works just fine, exactly like var. And basically, that's true: var and let do the exact same thing. You can more or less use them interchangeably.

The difference has to do with variable scope. To show you, let's go over to play.js and on top, let's add something silly: if (true), then aGreatNumber = 42, which of course is a great number. If we try this, of course it reassigns the variable to 42. All right. What if we said var aGreatNumber = 42? My question is, does that give an error? Does that change anything? The answer is no. We only need this first var ... you need the var to initialize the variable, but JavaScript is okay if you try another var down here. What this doesn't do is create a new variable. That's because the scope of variables created with var is whatever function they are in. Since neither of these are in any function, they share the same scope.

Now if you're not understand what I'm talking about, try this out. Let's wrap this var in a self-executive function. I'll use the new arrow function syntax and basically we're going to do that. We're creating an anonymous function, and then we're executing immediately. We should set aGreatNumber to 10 on top, then immediately we should change it to 42, and ultimately when we print, it should print as 42, right? Wrong. What? Remember, the scope of a variable created with var is whatever function it is inside of. Now that this is inside of a new function, when we say var aGreatNumber, it actually creates a new variable, and this new variable's scope is only this function. In other words, aGreatNumber inside of this function is not the same as this variable here. Setting this to 42 does not affect this variable up here. This is an edge case. You probably didn't even realize this happened, but it starts to describe the difference between var and let.

Let me show you. Remove the self-executing function and let's change both of these vars to let. If let and var were exactly the same, we would expect this, just like before, to be 42. But it's 10, and this is the key difference between var and let. For PHP developers, it's a little strange. In PHP and with var, we expect the variable scope to be whatever function we're inside of right now, including any embedded functions that we might have inside of that. However let is what is known as block-scoped, meaning anytime you have a new curly brace, opening curly close curly, like an if statement or a for loop, that is a new scope. In the way that we could create a brand new var variable inside of an embedded anonymous function, we can create a brand new aGreatNumber variable inside of this block. This new variable is different than the original one.

If we remove the let, now we get 42. This is because without the let, we're not trying to create a new variable, we're just saying change whatever the existing variable is to 42. If this is all making your head spin, that's okay. It turns out in practice, other than a few edge cases, var and let behave basically the same. If you want to learn about those use cases, those edge cases, and see how they work, I encourage you to go and research, but for the most part var and let are interchangeable.

There's one other reason why you might want to use let instead of var, and to show it off, I'm going to do something silly on top of this file. I'm going to try to console.log bar, which is just something I made up right now. That's not a real variable. If we try this, we get a ReferenceError, "bar is not defined." We don't get an undefined, we get a ReferenceError. It is an error. And no surprise. In fact, if we change this to aGreatNumber, the same thing's going to happen, because have not initialize that variable yet. If you change this to var, all of a sudden, it doesn't break anymore. It simply says that that value is undefined.

The reason for this is something called variable hoisting, which is a terminology you'll see a lot around JavaScript, and it's not actually that important, so I want to tell you a little bit about it and then you don't have to worry about it ever again. In PHP, we never have to initialize a variable with a special keyword. We don't have a var aGreatNumber = 10, we just say aGreatNumber = 10 and it's initialized and we're good to go. In lots of other languages, including JavaScript, you actually need to initialize the variable with a keyword.

With var, what variable hoisting is is it goes to whatever ... It basically means that right as JavaScript executes, it finds all of your vars, goes to the top of that variable's scope, so usually the top of whatever function it's inside of ... in this case, it's the top of the file, and effectively does this: var aGreatNumber. It initializes the variable, but it doesn't set it to any value. That's variable hoisting. In essence, other than some edge cases, it basically means that when you use var and try to use that variable before you've actually initialized it, you're not going to get an error.

If we change this to let, as we did earlier, we already know that that actually does throw the reference error. For the most part, that means that let works a little bit more like we expect it to work. It should throw errors if we're trying to use something that hasn't been initialized. Technically, let also has variable hoisting, but you get the ReferenceError due to something called a temporal dead zone, which again is a term you'll see all around this topic. I don't want you to worry about it because it's very low-level semantics. For us, what's important is that with let, our code is a little bit more predictable because we get good, solid errors if we try to do something legal.

Let's go into our rep log app. I'm going to change all of these vars to let. I'll even do a find and replace: var space for let space, replace all, and we should be good to go. Just to make sure that our code doesn't have any of these weird edge case differences between var and log, we can try it out. Everything looks like it's working just fine.

There's one other keyword that you're going to see which is const. So back in our play file, I'll get rid of aGreatNumber. Instead of let I will say const, and as you're probably already guessing, and you see from PhpStorm being very angry, the idea of a const is that it can't be reassigned, it can't be modified. We try this now, we're going to get a huge error, "Assignment to constant variable." If we just comment this out, it works just like we expect. As far as scope goes, const and let are identical. Const and let are the exact same thing, except that you can't modify a const. Well, let's define what we mean by modify a const. Let's create another const called aGreatObject. The key is called withGreatKeys, set to true, and then we'll say aGreatObject.withGreatKeys = false. We'll actually modify that object, and then we'll try to log it down here. Will that work?

Well, actually yes, and you can see withGreatKeys set to false, so it actually overrides it. When you use a const, it's not that the value that it's assigned to can't change. The object can change, it's just that literally you cannot reassign the aGreatObject to something else in memory. It has to be assigned only once to this object, but then this object can change.

We have var, let, and const, and there are some differences, but a lot of times you're going to see people using one or the other just purely based on personal preference. In our case, just to be super-hipster, we're going to change all of our lets to const. Start at the top. Let's go through these one by one, so const $link makes sense. We don't need to reassign that. deleteUrl, row, $form, and formData ... this one's interesting because that's an object and we do modify the object, but we know that is okay with a const. errorData, $form, fieldName, $wrapper, $error ... this is another case where this is an object that we will actually call some methods on and modify internally, but that's okay. Then we'll do just a couple more, until we get to the last one, totalWeight. This is actually the one case in our code right now where const doesn't work because we're setting it to 0, and we're actually reassigning it every loop through. That is the one spot we need to actually keep as a let.

All right, let's give this a try. Let's refresh the page. Delete something, everything works just fine. So var, let, const. Pick your favorite, use it everywhere.