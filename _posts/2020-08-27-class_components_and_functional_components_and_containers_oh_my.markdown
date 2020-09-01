---
layout: post
title:      "Class components and functional components and containers, oh my!"
date:       2020-08-27 15:03:48 -0400
permalink:  class_components_and_functional_components_and_containers_oh_my
---


When I started building my first application with React using Redux, I had learned the basics of React and thought I understood the pretty basic concept of different types of components.  Some components are basically functions, some are classes, more similar to a Ruby class, and some are containers that hold and render other components.  Great, easy, moving on.

It turns out there's a lot more to it than that, as I found out the hard way.

To start with, different types of components are set up differently, I knew that.  For example, since a Functional Component is a JavaScript function, it would be set up like a regular JS function:

```import React from 'react';

const HomePage = (props) => {

    return (
        <h1>
				Hello World!
        </h1>
    );
};```

Class components, on the other hand, require different syntax altogether.  First, it requires you to extend React.Component from React to access the class component properties from the React library.  It then needs a single render function with a return statement explicitly set.

```import React, { Component } from 'react';

class ProductsList extends Component {      
    
    render() {
        return (
            <div>
						Hello World!
						</div>
						)
			};```

Container components are class components, so they are constructed using the "class" keyword also, and follow the same rules as Class components do regarding syntax.

This is where it starts to get trickier.  If you're using React, you're probably familiar with Javascript already, so in a functional component, you'd expect to write a function like so:

```function handleBtnClick() {
        console.log("clicked!" 
      }``` 

And you'd be correct.  However, in class components, you write a function like this:

``` showAvailability(product) {
        if (product.available) {
            return <ul >This product is currently available</ul>}
        else {return null}
    }```

Notice the lack of the keyword "function". The minor change in syntax can be confusing if you don't know to watch for it. 

A major difference between class and functional components is in the setting of state and props.  A Class component could have state declared and set in a constructor function. A Class component can also create props and pass them to children functions (such as a functional component). It's not *required* to do these actions, but you wouldn't do them in a functional component at all.  

Once inside your component, you access *props* differently.  Class components require you to use "this.props" while functional components can access them through just "props".  The reason for this is that a functional component, as stated above, is just a Javascript function.  Once you pass props from the parent component in as an argument, you can then access it throughout the function.

Functional components are also referred to as "stateless", because they do not have their own state. So no constructor functions there!

In either case, remember that components do not modify props!

I hope this helps difine some of the differences between component types!

Happy coding!


