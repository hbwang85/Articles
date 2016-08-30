#Redux
## Principles
* Everything that changes in your applicaiton including the data and the UI state is contained in the single object, we call state or state tree;
* The state tree is read-only. Every time you need to change a state, you need to dispatch an action. An action is a plain JavaScrip object, it is the minimal representation of the change to the detail. The only requirement for the action data structure is that it has `type` property, which is not `undefined`;
* 


### Pure and impure function 
```
// Pure functions
function square(x) {
  return x * x;
}
function squareAll(items) {
  return items.map(square);
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


