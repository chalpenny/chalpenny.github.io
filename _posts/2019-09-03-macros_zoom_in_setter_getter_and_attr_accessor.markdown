---
layout: post
title:      "Macros Zoom In: setter, getter, & attr_accessor"
date:       2019-09-03 23:04:09 -0400
permalink:  macros_zoom_in_setter_getter_and_attr_accessor
---


Metaprogramming is the process of using a program within a program.  It's a very cool feature, and one of the reasons  Ruby is such a powerful language.  The macros that are created return code (as opposed to data) which you can then use to write other methods.  It's essentially writing code to do work for you.  This is great, as it can be a very helpful tool when writing repetitive code.

Ruby comes with its own built-in macros.  Let's look at one that comes up frequently when defining classes - the family of attribute accessors, written as ```attr_accessor```,``` attr_writer```, and``` attr_reader```.

When instantiating (or creating) a new instance of a class, it's pretty common to want to be able to name that new instance.  This name is known as a property of that instance.  To set that property, you would need to write a method that would allow you to pass in an argument of a name for your instance.  

Let's look at how to do that in the following example.  Below, we have a class called BandMember.  When we instantiate a new instance of that class, we'll want to give this BandMember a name.  We're able to do it with the method shown inside our class:

```
class BandMember

def name=(name)
@name = name
end

end
```

Whoa, whoa, whoa.  That's a lot of names going on there.  What's happening?  Didn't we just want to give our BandMember one name?  

How does that method work?   This type of method is called a *setter* method (also called a *writer* method).  As the name suggests, we're *setting* our instance's name.  If we break it down into its parts, here's what we get:

```def name=(name)```

This is following the familiar pattern of defining a method:

```def method_name(argument)```

Note that our method is actually called "name=".  

Next is the body of the method:

```@name```


This is an instance variable.  Different from a local variable which is only recognized within the method it was created in, an instance variable is recognized and can be used in other methods throughout that instance of that class.


```@name = name```

Here we've set our instance variable, ```@name``` equal to our argument that was passed in, which in this case is the name of our BandMember.  Does that seem a little confusing to use the same word?  It can be, and it's not required for the method to work, but it's convention to write it that way.

So right now we've defined a method, called ```name=```, that accepts the argument of a name.  Within our method, we set that argument equal to an instance variable so that we can pass it around within the other methods we're going to create.  Great!  Now we can create a new instance of BandMember and give them a name:

```new_member = BandMember.new
new_member = "Ringo"```

The only problem here is that nowhere within our current code do we have a way to access the name we created.  So if we want to know the name of our BandMember is, we have no way to call it!  This is where we create what's called the *getter* method (also known as a *reader* method). 

This way, we can get our info back out again when we need to.

```def name
@name
end```

Here we are using the same ```name``` word again.  How confusing!  But if we look closely, we can see that what's going on is pretty straighforward:

```def name```

We've defined our method as "name".

```@name```

When this method gets called, it wil return the ```@name``` instance variable, which you'll remember we set already with the name that was passed in earlier.

And that's it!  It makes sense now. We can set our name, and we can get our name.

Since this is such a common procedure, Ruby makes our lives easier by allowing the use of a macro that, with a few simple words, will do all of that code for us.  There's the attr_writer for the setter/writer method, the attr_reader for the getter/reader method, and the attr_accessor, which is both methods rolled into one handy macro.  To use these macros, rather than using a method you would write it like this:

```class BandMember

attr_accessor :name, :age,: instrument
attr_reader :height

end
```

Depending on the makeup of our method, you may have LOTS of properties.  Or you may only have one.  You may need just the reader if your information won't change once it's initially set (like someone's birth date),  or maybe just the writer if you don't need to access it outside of your instance method, or a combination of all three.

You can see why using Ruby's attribute accessor method to write all that repetitive code for us can save a lot of time.  It's quick, easy, and avoids the possibility of a little mistake messing up your program.

Happy coding!



