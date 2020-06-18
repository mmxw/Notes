
- use `deepFreeze` to freeze objects so that they cannot be mutated
- use the following methods to avoid mutations of arrays or objects

```js
arr = [0, 1]

❌ arr.push(2) 
✅ arr.concat([0]) // `arr` is not mutated
✅ [...arr, 0] // or use spread operator

❌ arr.splice(index, 1)
✅ arr.slice(0, index).concat(arr.slice(index + 1)) 
✅[...arr.slice(0, index), ...arr.slice(index + 1)]

❌ arr[index]++
✅arr.slice(0, index).concat([arr[index] + 1].concat(arr.slice(index + 1))
✅[...arr.slice(0, index), arr[index] + 1, ...arr.slice(index + 1)]

//for object mutations:
const todo = {a: 1, b: 2}
Object.assign({}, {b: 3, c: 4, d: 5}) // returns {a: 1, b: 3, c: 4, d: 5}

//but Object.assign() is not available on all browers (e.g., IE, baidu, qq, opera mini etc.), in this case, use spread operator to avoid website crashing

{...todo, b: 3, c: 4, d: 5}

deepFreeze(arr) 
```


