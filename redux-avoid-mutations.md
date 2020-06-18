### Avoid mutating state objects in redux

From Redux [docs](https://redux.js.org/introduction/three-principles): 
> Changes are made with pure functions

> To specify how the state tree is transformed by actions, you write pure reducers.

> Reducers are just pure functions that take the previous state and an action, and return the next state. Remember to return new state objects, instead of mutating the previous state. You can start with a single reducer, and as your app grows, split it off into smaller reducers that manage specific parts of the state tree. Because reducers are just functions, you can control the order in which they are called, pass additional data, or even make reusable reducers for common tasks such as pagination.

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
