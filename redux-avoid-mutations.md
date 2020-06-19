### Avoid mutating state objects in redux

From Redux [docs](https://redux.js.org/introduction/three-principles): 
> **Changes are made with pure functions**

> To specify how the state tree is transformed by actions, you write pure reducers.

> Reducers are just pure functions that take the previous state and an action, and return the next state. Remember to return new state objects, instead of mutating the previous state. You can start with a single reducer, and as your app grows, split it off into smaller reducers that manage specific parts of the state tree. Because reducers are just functions, you can control the order in which they are called, pass additional data, or even make reusable reducers for common tasks such as pagination.

From [Idiomatic Redux: the history and implementation of React-Redux](https://blog.isquaredsoftware.com/2018/11/react-redux-history-implementation/): 

> **UI Updates Require Store Immutability**

> We've already established that the Redux store will run all subscriber callbacks after every dispatched action, regardless of whether the state actually changed or not.

> In order to implement efficient UI updates, React-Redux assumes you have updated the store state immutably, so it can use reference comparisons to determine if the state changed.

> This occurs in three stages:

> - When a connect wrapper component's subscriber callback runs, it first calls store.getState(), and checks to see if prevStoreState !== storeState. If the store state did not change by reference, then it will stop right there and bail out of any further update work, because it assumes that no other part of the store state changed.
- If the root state has changed, the wrapper component then runs your mapState function, and does a "shallow equality" comparison between the current result and the last result. If any of the fields have changed by reference, then your component probably needs to be updated.
- Assuming that there was some change in the mapState or mapDispatch results, the mergeProps() function is run to combine the stateProps from mapState, dispatchProps from mapDispatch, and ownProps from the wrapper component itself. A final check is done to see if the merged props result has changed since the last time, and if there's no change, the wrapped component will not be re-rendered.

> Note: The root state comparison relies on a specific optimization in combineReducers, which checks to see if any state slices were changed while processing an action, and if not, returns the previous state object instead of a new one. This is a key reason why mutating your state results in your React UI components not updating!

### Here are some ways of avoiding mutations of the previous state objects: 

- use `deepFreeze` to freeze objects so that they cannot be mutated
- use the following methods to avoid mutations of arrays or objects

```js
arr = [0, 1]

❌ arr.push(2) // mutates `arr`
✅ arr.concat([2]) // `arr` is not mutated
✅ [...arr, 2] // or use spread operator

❌ arr.splice(index, 1) // mutates `arr`
✅ arr.slice(0, index).concat(arr.slice(index + 1)) // `arr` is not mutated
✅[...arr.slice(0, index), ...arr.slice(index + 1)] // `arr` is not mutated

❌ arr[index]++ // mutates `arr`
✅ arr.slice(0, index).concat([arr[index] + 1].concat(arr.slice(index + 1)) // `arr` is not mutated
✅ [...arr.slice(0, index), arr[index] + 1, ...arr.slice(index + 1)] // `arr` is not mutated

//for object mutations:
const todo = {a: 1, b: 2}
✅ Object.assign(todo, {b: 3, c: 4, d: 5}) // returns {a: 1, b: 3, c: 4, d: 5}

//but Object.assign() is not available on all browers (e.g., IE, baidu, qq, opera mini etc.)
//in this case, use spread operator to avoid website crashing

✅ {...todo, b: 3, c: 4, d: 5}

deepFreeze(arr)

```

**Reference**: Dan Abramov's Redux [tutorial](https://egghead.io/courses/getting-started-with-redux) on egghead
