---
layout: post
title:      "MapStateToProps & MapDispatchToProps - what are they doing, anyway?"
date:       2020-09-04 12:33:16 -0400
permalink:  mapstatetoprops_and_mapdispatchtoprops_-_what_are_they_doing_anyway
---


You may have seen the use of one or both of these functions listed near the end of a component in a Redux app.  What exactly are they doing there?  Their names are quite descriptive, yet somehow don't convey exactly what it is they DO.  Let's unravel their path through an app.

First off, MapStateToProps and MapDispatchToProps are two functions that are passed as arguments to *connect()*.  To understand what their purpose is, we have to understand what connect() is.

As the name would suggest, connect() is used to connect a component to Redux (and the store). Ideally, our componnents are not aware of Redux.  They just get to focus on doing their own component-y thing.  Connect() gives us that separation of concerns that we're looking for.

The first argument it takes is MapStateToProps.  Its job is to provide only the parts of our store's state to the component that it needs, thus avoiding unneccesary changes to state (and unneccessary updates to the DOM).

MapState takes an argument of the store's state.  It's called every time that state changes, and returns the new state data that you've defined.

```const mapStateToProps = state => {
    return {
        products: state.products
    }
};```

In the example above, by passing in state as an argument, we can then set the key of products to be just the state.products information, which it returns as an object. Each key you define becomes a prop for your component. This will strip away any extraneous info in state that we don't need in this component.

When changes occur to those props, connect can then determine if the store state has changed and if it needs to re-render/update the DOM.

The second argument is MapDispatchToProps.  Map Dispatch is a function that triggers an action to update the store.  Dispatching is the only way to trigger actions, so by adding this function to a component, you are giving that component the ability to update the store.  As this will trigger updates to the DOM at certain points, you will want to be sure you're using it only when needed.  (Remember, updating the DOM takes time and can slow down your app if it's done frequently.  We want to keep it at the minimum required).

Once you import connect(), whether you know it or not you now have access to dispatch.  In the export statement, if you don't specify the second argument for connect(), it will default to *dispatch*.

```export default connect(mapStateToProps)(ProductPage);```

is actually

```export default connect(mapStateToProps, dispatch)(ProductPage);```

So your component will have access to dispatch as soon as you use connect().

You can also write your own MapDispatch function.  For example, if that component only needs to dispatch one particular action, you can write your MapDispatch function to dispatch that action only.  Keep in mind, however, that once you define your own function for MapDispatch, it no longer passes *dispatch* as a default.

To define your own MapDispatch function, you will pass dispatch as an argument, then return the action creator(s) you want access to:

```const mapDispatchToProps = dispatch => {
  return {
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrement: () => dispatch({ type: 'DECREMENT' }),
    reset: () => dispatch({ type: 'RESET' })
  }
}```

Because of how smart Redux is, you can even import an action creator directly to your component, as in:

```import { updateProductStatus } from '../actions/updateProductStatus';```

and then pass it as your MapDispatch argument in your export statement, which will then make it accessible as props:

```export default connect(null, {updateProductStatus}(UserCart); ```

Or pass just the action creators:

```const actionCreators = {
  increment,
  decrement,
  reset
}```

and 

```export default connect(mapState, actionCreators)(Counter);```

(Note that you can call MapDispatchToProps whatever name you want).

These two functions passed to connect() serve to "hook up" a component with the tools neccessary to keep a separation of concerns, and to avoid your componets from interacting directly with your store!

Happy coding!





