---
layout: post
title:      "Class components and functional components and containers, oh my!"
date:       2020-08-27 19:03:47 +0000
permalink:  class_components_and_functional_components_and_containers_oh_my
---


When I started building my first application with React using Redux, I had learned the basics of React and thought I understood the pretty basic concept of different types of components.  Some components are basically functions, some are classes, more similar to a Ruby class, and some are containers that hold and render other components.  Great, easy, moving on.

It turns out there's a lot more to it than that, as I found out the hard way.

The components are set up differently, I knew that.  For example, a class component 

EXAMPLE OF CLASS AND FUNCTIONAL COMPONENTS

Container components are class components, so they are constructed using ____ and follow the same rules.

This means that you need to access *props* differently.  Class components require you to use "this.props" while functional components can access them through just "props".  The reason for this is that a functional component, as stated above, is just a Javascript function.  Once you pass props from the parent component in as an argument, you can then access it throughout the function.

EXAMPLE 

Functional components then return a React element.

Class components, on the other hand, require different syntax altogether.  First, it requires you to extend React.Component from React to access the class component properties.  It then needs a single render function with a return statement explicitly set.

EXAMPLE

This is where it starts to get trickier.  If you're using React, you're probably familiar with Javascript already, so in a functional component, you'd expect to write a function like so:

EXAMPLE 

And you'd be correct.  However, in class components, you write a function like this:

EXAMPLE

The minor change in syntax can be confusing if you don't know to watch for it.  Another small note - even using the debugger can be confusing if you're not expecting this change.

EXAMPLE


