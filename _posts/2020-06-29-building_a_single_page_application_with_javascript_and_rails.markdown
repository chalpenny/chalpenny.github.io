---
layout: post
title:      "Building a Single Page Application with JavaScript and Rails"
date:       2020-06-29 03:07:52 -0400
permalink:  building_a_single_page_application_with_javascript_and_rails
---


After building a working application with Rails alone, I started out by wondering what JavaScript had to offer that I couldn't accomplish already.  While JS isn't required to make a webpage, it sure does offer some fun options.  Being able to make asynchronous requests ( HTTP requests to the server ) at the point in your code that it's needed speeds up your application as well.  JavaScript's lack of convention in modeling files is a bit of a double-edged sword; on one hand it leaves you pretty open to build your application in a way that makes sense to your project, but on the other it doesn't stop you from creating jumbled code either.

One thing that JS offers that felt familiar to Rails is its use of OOJS, or Object Oriented JavaScript.  You can use classes or prototypes to create a JS object, which then allows you to access attributes, create associations, and encapsulate functions.  JS classes are in fact functions, but they operate similarly enough to a Rails object that when you're first getting started, it may help to think of them that way.  

Once you decide to use OOJS in your application, it's best to create a *src* folder and create new .js files for each class you use.  This will help with clarity down the road, and keep your code understandable.  

Next, create your class:

```class Activity {

    constructor(data) {
        this.id = data.id
        this.name = data.name
        this.url = data.url
        this.notes = data.notes
        this.category_id = data.category.id
        Activity.all.push(this)  
    }
}

Activity.all = []
```


Be sure your attributes here match the attributes on your backend model.  You'll notice the use of the keyword *this* in our constructor.  *This* is similar to *self* in Ruby in that it refers to whatever instance it is part of.

An important thing to note is that the attribute names on the left of the = need to match exactly your backend attribute names.  The attribute names on the right of the = are JS and just need to work within your own JS code.

You now have the ability to create new JS objects in your code!

A very common usage for an object would be to use it in a fetch request:

``` 
fetch (ACTIVITIES_URL, configObj)
        .then(function(resp){
            return resp.json()
        })
        .then(function(data){
            let newActivity = new Activity(data)
            makeActivityList(newActivity, newActivity.category_id)                
        })
				```


The line 

let newActivity = new Activity(data)

is calling the *new* action / create action on your Activity class, using the data returned by the fetch as parameters to build your object (the attributes in your class). [Note that the argument *data* here does not have to be the same argument name in your class.  You're passing arguments as you would in any other function]

You'll note that immediately after creating the new Activity instance, a function *makeActivityList* is called on it.  One option that classes allow is to create a function AS PART OF THE CLASS.  If every instance of that class will have the same function called on it, you can encapsulate that action within the class itself.

```
class Hero {
    constructor(name, level) {
        this.name = name;
        this.level = level;
    }

    greet() {
        return `${this.name} says hello.`;
    }
}
```

In the example above, you see that every instance of this object will have a *greet* function.


Now that you have a class, you can begin to use associations with it.  If we were to create merely an object, not a class from the returned json data in our fetch method above, we wouldn't have to advantage of those associations.  With the appropriate has_many, etc ActiveRecord associations in your backend files, you can now call things like *activity.category_id* to see its belongs_to relationship.

One last note about JS classes is that they are not a new feature, they existed in versions before ES6 as *prototypes*.  Constructed and used similarly, classes are merely syntactic sugar, designed to make a coder's life a little easier!

