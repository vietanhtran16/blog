---
title: Redux 101
date: "2018-01-10T16:51:00.000Z"
layout: post
draft: false
path: "/posts/redux-101/"
category: "react"
tags:
  - "react"
  - "redux"
description: "The basics of Redux"
---

Redux in simple term is a state container for JavaScript apps - not just for React. 

It allows consistency in your application since state of the whole application is store in a single immutable tree. Since it is immutable, the only way to update the state is to dispatch an action using a pure functions.

## Basics of Redux
### Actions
* Information that describes what type of action should be performed and what part of the state should be updated
* Describes what just happened in the application
* Due to that, _Type_ property is a must-have in an action which would normally be a string constant
* The other property could be optinal based on what properties of the state you want to update

```javascript
//An action to add item to a note list
{
    type: "ADD_NOTE",
    text: "Set up meeting",
}
```

### Action Creators
* Are functions that create actions
* The results (actions) would then be passed into _dispatch_ function to update the state of the store

```javascript
//Action creator for ADD_NOTE action
function addNote(text){
    return {
        type: "ADD_NOTE",
        text,
    }
}

//Call dispatch to add note to store state
dispatch(addNote(text));
```

### Reducers
* Tranform current store state to the new state based on the actions
* This is how store state is updated in Redux
* Should always be pure functions - no side effect store state

```javascript
function reducer(currentState, action){
    //Do something to update the state
    return newState;
}
```


_myNote_ reducer has _initialState_ as it default store state. Inside the function, it looks at the type of the _action_ to determine how store state is update. A completely new state object is returned by concatenating the current notes with the additional note from action. The changes should never be applied directly to the state but we should always return a new object to maintain its immutability.

```javascript
//Create initial state of the store
const initialState = {
    notes: [],
};

//myNote reducer
function myNote(state = initialState, action){
    switch(action.type){
        //Update notes property of store state
        case "ADD_NOTE":
            return {
                    notes: [
                        ...state.notes,
                        action.text
                    ] 
                }
        default: 
            return state;
    }
}
```

### Splitting and combining reducers
Since your whole application has a single store, the store would have information of multiple parts of your application. If only one reducer handles state changes of the whole application, it will get out of hand very quickly. We could split the reducer so that each reducer handle a portion of the store state then use _combineReducers_ to merge them into one.

```javascript
//Initial state of the store
const initialState = {
    notes: [],
    displayOnlyFive: false,
};

//Reducer that handles notes property of store state
function notes(state = [], action){
    switch(action.type){
        //Update notes property of store state
        case "ADD_NOTE":
            return {
                    notes: [
                        ...state.notes,
                        action.text
                    ] 
                }
        default: 
            return state;
    }
}

//Reducer that handles displayOnlyFive property of store state
function displayOnlyFive(state = false, action){
    switch(action.type){
        case "DISPLAY_ONLY_FIVE_NOTES":
            return action.displayOnlyFive;
        default: 
            return state;
    }
} 

//Combine reducers
const myNote = combineReducers({
    notes,
    displayOnlyFive,
});

//Which is the same as this
function myNote(state = {}, action) {
  return {
    notes: notes(state.notes, action),
    displayOnlyFive: displayOnlyFive(state.displayOnlyFive, action)
  }
}
```

### The lifecycle
1. _store.dispatch(action)_ is called to send action object to the store
2. The store will then pass current state and the action to the reducer
    * The reducer will then return the next state
    * _dispatch_ knows which reducer to use since we already wired up the reducer with the store as below
3. Multiple reducers can be merged into one to create the state tree
4. The store then saves the new state returned from the reducer
    * Listeners that have been subscribed to the store will be invoked
    
```javascript
const store = createStore<IStoreState>(reducer);
```


*Reference:* [Redux](https://redux.js.org/)
