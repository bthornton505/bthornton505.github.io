---
layout: post
title:      "What's Redux and Why do you Need It?"
date:       2019-04-26 20:23:02 +0000
permalink:  whats_redux_and_why_do_you_need_it
---

You may be asking yourself "Why do I need this Redux thing everyone keeps talking about?" and depending on your current project, you may not need Redux. But there are very good reasons to consider implementing it into your application. Let's find out why...

## Welcome to Redux

Simply put, Redux is a JavaScript tool that allows a developer to manage their applications state in a predictable state container. This type of tool comes in handy when your application starts to scale up and becomes overall more complex.

At some point, you no longer understand what happens in your app as you have lost control over the when, why, and how of its state. This makes React and Redux somewhat of a perfect match for each other with Redux managing the application state and React components connecting to this state tree to use the data as needed. 


## Installation

There's a couple ways to get this installed into your project but the most straight forward would be to use a package manager such as NPM. If you don't have this I would suggest downloading it now cause it will make life significantly easier. 

With NPM just run this line of code:

`npm install --save redux`

And you'll be ready to go for the setup of Redux in your application!


## Actions 

To get started we need to establish what we will be doing to our applications state. The process of updating our state is comprised of sending Actions which then go to Reducers who then decide how the state is going to be updated. 

Let's start with Actions.

Actions are objects that contain payloads of data that are sent from your application to the store. This is the only way to send information to the store. Here's an example:

```
const ADD_TODO = 'ADD_TODO'

{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
```

From the example above you can see that Actions are JavaScript objects which contain an action type and the payload created. Actions are required to have a type property which indicates the type of action performed. In the first line you can see that this type is being declared as a string constant. You can then use this constant when declaring the action. 

Once this type has been declared in the action, you are free to construct your action however you want. So with the basics setup we can move into Action Creators.

Action Creators are functions that return an action. This makes them portable and easy to test. 

```
const addTodo = (text) => {
  return {
    type: ADD_TODO,
    text
  }
}
```

In Redux you need to take these Actions and pass them to the `dispatch()` function which will initiate the change. This is availble through the use of a helper provided by react-redux's `connect()`. 

`dispatch(addTodo(text))`

As your app grows, you may need to make api calls. Actions can be asynchrounus, allowing them to handle AJAX requests and turning your action creators into async actions. If you're curious about this more advanced form of Redux check it out here https://redux.js.org/advanced/async-actions

Next let's define some reducers which will specify how to update the state when these actions are dispatched.


## Reducers

After you've declared your actions you need to build a Reducer to handle updating your applications state. Actions only declare what changes need to be made but can't actually make the changes. This is where Reducers come into play.

The Reducer is a pure function which takes the previous state, the action, and returns the next state.

`(previousState, action) => newState`

It's called a reducer because it's the type of function you would pass to `Array.prototype.reduce(reducer, ?initialValue)`. There are a few things never to do when building your reducers:

* Mutate its arguments;
* Perform side effects like API calls and routing transitions;
* Call non-pure functions, e.g. Date.now() or Math.random()

So with that said, a Reducers should always be a pure function. This means it will reliably return the same result every single time. Now lets teach our Reducers how to handle the actions that are sent to it.

The first step is to establish the inital state. Redux will call our reducer with an `undefined` state on the first try. So let's define it:

```
import { VisibilityFilters } from './actions'

const initialState = {
  visibilityFilter: VisibilityFilters.SHOW_ALL,
  todos: []
}

const todoApp = (state, action) => {
  if (typeof state === 'undefined') {
    return initialState
  }

  // For now, don't handle any actions
  // and just return the state given to us.
  return state
}
```

With ES6 we can use the default argument syntax like so:

```
const todoApp = (state = initialState, action) => {
  // For now, don't handle any actions
  // and just return the state given to us.
  return state
}
```

Now lets handle the change our state by building a Switch/Case conditional:

```
function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return { ...state, visibilityFilter: action.filter }
			
    default:
      return state
  }
}
```

A couple important things to point out above:

* We don't mutate the state. By using the spread operator we copy over the enumerable objects from one to another. 
* We return the previous state in the defalut case. This will handle any unknown actions that are passed to the reducer. 

With this setup it's very easy for your reducer to become very verbose. Redux has a great way to handle this issue. Take the following code sample:

```
const todoApp = (state = initialState, action) => {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: [
          ...state.todos,
          {
            text: action.text,
            completed: false
          }
        ]
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: state.todos.map((todo, index) => {
          if (index === action.index) {
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      })
    default:
      return state
  }
}
```

In this situation it seems as though we can easily separate updating todos into another function.

```
function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}

function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    case ADD_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    case TOGGLE_TODO:
      return Object.assign({}, state, {
        todos: todos(state.todos, action)
      })
    default:
      return state
  }
}
```

This separation of reducer functions is called Reducer Composition. You can see that now todo has a slice of the state to take care of and it's passing an empty array as it's default argument. This is a key fundamental of Redux. 

We can go a step further with this code and separate the visibility filter into its own reducer function like so:

```
const { SHOW_ALL } = VisibilityFilters

function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}
```

We then take the main reducer function and have it call the newly created reducers in an object.

```
function todoApp(state = {}, action) {
  return {
    visibilityFilter: visibilityFilter(state.visibilityFilter, action),
    todos: todos(state.todos, action)
  }
}
```

In Redux, however, we can use something called `combineReducers()` to make this a lot cleaner. When your app grows you would take these separate reducer functions and place them into their own files. This keeps them separate and allows them to manage their own piece of the applications state. This is where we use the utility `combineReducers()`. 

```
import { combineReducers } from 'redux'

const todoApp = combineReducers({
  visibilityFilter,
  todos
})

export default todoApp
```

Here we use `combineReducers()` to generate a function that calls your reducers. 

Now with your Actions and Reducers setup, lets create a Redux store. This will hold your state and takes care of calling your reducer when actions are dispatched. 


## Create your Store

The Store is the object that brings together your actions and reducers. It has a list of responsibilities:

* Holds application state;
* Allows access to state via `getState()`;
* Allows state to be updated via `dispatch(action)`;
* Registers listeners via `subscribe(listener)`;
* Handles unregistering of listeners via the function returned by `subscribe(listener)`

One important thing to remember is you will only have one Store in your Redux application. Reducer composition will be used to split your data handling logic. 

Creating a Store is pretty simple. Previously we used `combineReducers()` to combine several reducers. We can import this and pass it to `createStore()` which will create your store.

```
import { createStore } from 'redux'
import todoApp from './reducers'

const store = createStore(todoApp)
```

Now your Store has been created and it will be able to take the Actions dispatched with the Reducers handling the update of state. 


## Three Main Redux Principles

Before we wrap up lets talk about three main principles of Redux:

### 1. Single Source of Truth

The state of your whole application is stored in an object tree within a single store.

Redux holds your applications state in one store which manages everything for you. A single state allows for easier debugging and inspection of your app. Creating an easier work flow during development.

### 2. State is Read-Only

The only way to change the state is to emit an action, an object describing what happened.

This is a huge principle in Redux because the idea is to never mutate the state directly. Actions are an intent to transform the state in a centralized location. These changes happen in a strict order which provides a reliable system that produces consistent results. 

### 3. Changes are made with pure functions

To specify how the state tree is transformed by actions, you write pure reducers.

Reducers are pure functions which take the previous state, an action, and return the next state. This is the flow of Redux and it creates a system that can be very reliable when developing an application. As your app grows you can split your reducer up into smaller reducers that manage slices of the state. This allows for organization within the store. 


## So Why Redux?

That was a lot to process and honestly I had quite a bit of trouble implementing Redux for the first time. There are a lot of aspects to think about when connecting your React components to the store. A good way to think of Redux is that it sits on top of your entire React application. Just look at how you provide the store to your application:

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import rootReducer from './reducers/index.js'

const store = createStore(rootReducer)

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

You can see from this example that your store is passed as a prop to the Provider which is imported from `react-redux`. This just goes to show how much Redux really is a manager of your applications state. React components connected to the store will dispatch actions and wait for Redux to handle the update to state. 

This tool can be very useful as your application starts to grow and more specifically when you get into async actions. Redux also provides a very useful developer tools that can be used in the console to watch the order of changes to your state. Debugging becomes significantly easier with these tools and gives you a visualization of your apps state. 

Hopefully this article has given you a foundation of how Redux works and why it could be useful in your next project.

For further documentations I highly recommend Redux's docs: https://redux.js.org/introduction/getting-started

