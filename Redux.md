#Redux
## Principles
* Everything that changes in your applicaiton including the data and the UI state is contained in the single object, we call state or state tree, The state of your whole application is stored in an object tree within a single store;
* The state tree is read-only. Every time you need to change a state, you need to dispatch an action. An action is a plain JavaScrip object, it is the minimal representation of the change to the detail. The only requirement for the action data structure is that it has `type` property, which is not `undefined`;
* To specify how the state tree is transformed by actions, you write `pure reducers`.


### Pure and impure function 
```
// Pure functions
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square); // do not override the `item`, 									  //instead it returns a new array
}

// Impure functions
function square(x) {
  updateXInDatabase(x);
  return x * x;
}
function squareAll(items) {
  for (let i = 0; i < items.length; i++) {
    items[i] = square(items[i]);
  }
}
```
#### Pure functions
* The pure functions are the functions whose returned value depends solely on the value of the arguments. 
* Pure functions do not have the observable side-effects, such as network or database calls. 
* The pure functions just calculate the value and you can be confident that if you call the pure function with the same set of arguments you will get the same return value. 
* They are predictable.
* They do not modify the values pass to them.

#### Impure functions
* They may call the network or the database, they may have the side-effects, they may override the value passed to them		

####Reducer function
* The reducer is a pure function that takes the previous state and an action, and returns the next state.

 ```(previousState, action) => newState```
* [Express Library](https://github.com/mjackson/expect)

####Store methods
```
const { createStore } = Redux;
var createStore = Redux.createStore;
import { createStore } from 'redux';
const store = createStore(counter);
```
##### 3 important methods
* getState()
* dispatch()
* subscribe()



