# Class Syntax

Alright, in the first episode we talked about objects, real objects and we learned that you can actually create real objects in JavaScript by actually creating a function which acts as the constructor. Then adding all of the real methods and properties to the prototype. This uses JavaScripts' prototypical inheritance.

Mentioned in the first episode that, this means that there aren't any classes like there are in PHP. Well, that's not actually true. Ecmescript 2015 introduces one of the most important and big features of classes, true classes. So lets actually see what they look like.

If you're a PHP developer like I am, you're actually going to love what classes look like. Cause, if we want to create a helper class we say, class helper. And then we say open curly, close curly. That is a class in Java Script. Just like it's a class in PHP.

Now like PHP we have constructors. In JavaScript the constructors actually called just constructor. So I'll move our old constructor function up here and we are gonna rename this to simply constructor. Then we can get rid of the semicolon afterwards because now this is just a method. And now we can very easily move everything else into it by getting rid of $.extend helper.prototype and just adding all these as methods inside of here. And congratulations we have created a new Ecmescript 2015 class. Wasn't that easy?

In fact it works the exact same way as before. So everything still works still calculates the total. Everything is exactly the same. In fact the reason it's exactly the same is this new class setup is just a new syntax. Behind the scenes JavaScript still follows the prototypical object oriented model. This is just a nice wrapper around it. So that you don't have to worry about setting the prototype, this sets all that for you behind the scenes. So especially for us PHP developers, this is a whole lot more familiar, but ultimately nothing has changed behind the scenes.

So let's do the same thing up here with our RepLogApp. So now, I'll say class RepLogApp, open curly, and then I'll make this right here, of course our constructor. Which you'll want to make sure that you actually spell correctly. I'll indent everything and that will add the closing curly brace. Cool? So there is our constructor. And then we just need to move in all the other methods.

But, before we do that, I'm actually just gonna start with this selectors property here. Let's go up here, paste that and immediately you can see that it is super angry. It says: "types are not supported by current JavaScript version." What it's trying to tell you is, to tell us is ... When you use this class syntax, properties aren't supported. Only methods are supported, and that's actually on purpose. Properties are actually a bit frowned upon inside of classes and objects. Instead we should use methods. So I mean is very simply were just going to change this to a method called GIT. Underscore GIT selectors. And if we do that, and then add a return, if we do that everything is happy. Well everything except for the couple places where we used the selectors. So you can see this._selectors, that's not gonna work, because we changed that to be a method. But I'm actually not gonna fix that now. We are gonna coma back and fix that in a second.

First, once I'm actually finish converting everything else to methods instead of a object. So, let's move down up here, we can get rid of the comas after all the methods. But other than that, nothing really changes.

So just make sure we didn't totally messed something up. And everything looks fine. I mean, it's just that simple. So now let's go back and worry about this, getSelectors thing because of course we have all of our broken calls to this._selectors. So, I would say the easiest thing to do would be to just change this and anything else that uses this old property names, to this ._getselectors.

But instead, check this out. And in front of ... I actually want you to change this back to _selectors and then in front of it type "get" space. And you can see instantly that PHP Storm is not angry because that is a valid syntax. And when you search for _selectors, you can see that PHP Storm is not longer unhappy about this. So this "get" syntax, is a special thing from Ecmescript 2015, which allows you to define a method that should be called, when somebody tries to get the _selectors property. And there's also a "set" version of this. That if somebody, so somebody can set a _selectors property. So even though are classes don't support properties, we can actually create things so that people can use what looks like properties on us, but internally is gonna called this get instead of methods.

All right, so after all these changes, let's go back and try this. And actually you'll see that it won't work. The reason is we get RepLogApp is not defined, coming from our actual template itself. Resources app, resources views, index.html.twig. Down here at the bottom. So this is where we [inaudible 00:07:20] our RepLogApp object. The problem is, that this class only lives within this self executing function. So it's actually the same problem we had earlier with scope, and we are solving it the same way we did earlier which is we need to re-export this to the global scope by saying window.RepLogApp equals RepLogApp. Now, life is good again.

So taking it back now at that new get_selectors, and if you see PHP Storm has it highlighted like there's something wrong. If you hove over it, it says method can't be static. So when we talk about objects in the first episode, I talked about how when you use prototypical inheritance, it's like creating true methods on objects. Because you can create new instances of those objects. And every instance of an object is gonna have its own internal data. And I also said, if you decided not to put a method on the prototype, that's legal but it affectively becomes static. Now, if this didn't make a lot of sense it's okay because it's a little bit weird for us as PHP developers to try to think about static vs non-static, and also how this works into prototypical object model.

Well, the good news is, with this new format, JavaScript has made the idea of static and non-static much easier. PHP Storm has simply set, telling us that this method can be static because it is not using the "this" variable. So that's the same thing in PHP. If a method doesn't use the "this" variable it could be made static if we wanted to. So, this is fine either way. Let's actually make the static by saying "static", get selectors. And as soon as we do that, we can't say this._selectors anymore. Now we are going to say RepLogApp._selectors. Same way in PHP that we were referenced static methods by the class name, not actually by the object itself. So we'll change it in few other places.Perfect.

It's time to go back and refresh. Still loads up just fine. So, let's actually see one more example of a static variable on a normal method. Let's go all the way down here, down the bottom on our helper class. And I'm going to create a new method here called static_calculateweight which is going to take elements ... Array. And what I do, is basically I'm going to have a new utility method, who's job is to loop over whatever elements I pass it, look for their weight data [inaudible 00:10:36], add the map and return the total weight. So we don't need to do this because we are not going use this in multiple places, but this is a valid thing to do.

Now [inaudible 00:10:46] in calculated total weight, we can simply say, return Helper, cause we need to reference the static method by our class name, ._calculatetotalweight, and It'll pass it the elements that we wanted to find, which this.wrapper.find tbody tr. Okay, try that out and now we're still getting the correct total down here. [inaudible 00:11:32] For PHP developers this is huge because I can explain this 10 times faster, than I can be prototypical inheritance behind JavaScript. Now, the reason we went through that in the first tutorial, is ultimately JavaScript does still use prototypical inheritance, so you still need to understand that. But, now we can use this nice wrapper on top of it and it looks a lot cleaner to us.