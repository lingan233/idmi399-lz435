# 29. Execute Asynchronous Functions in Parallel
#### https://leetcode.com/problems/execute-asynchronous-functions-in-parallel/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### ime Taken: 3.5 hrs

This problem asks for the promise all function parallelly without using `promise.all()`.  

The problem works as follows:
- Return a new promise object
- Take the props and use the `.then()` on each of the promises to add a count for each successful promise
- If each promise is successful, then resolve the new promise object we created.
- If not, reject it.

Overall, this problem manually promises all promises. 

```javascript
/**
 * @param {Array<Function>} functions
 * @return {Promise<Array<any>>}
 */
var promiseAll = function(functions) {
  return new Promise((resolve, reject) => {
    const results = [];
    let completedCount = 0;

    functions.forEach((promise, index) => {
      promise().then(result => {
        results[index] = result;
        completedCount++;

        if (completedCount === functions.length) {
          resolve(results);
        }
      }).catch(error => {
        reject(error);
      });
    });
  });
};

/**
 * const promise = promiseAll([() => new Promise(res => res(42))])
 * promise.then(console.log); // [42]
 */
```

# 30. Group By
#### https://leetcode.com/problems/group-by/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 3 hrs

This problem asks to create a function that groups array based on the input `fn`’s requirement without using the default `groupBy` function. The problem gave helpful hint on how to solve it. 

The problem works as follows:
- Create an object
- Iterate through each item in the array.
- If there is no `obj[key]`, then we make it an empty array
- We push item into `obj[key]`

Overall, this function groups array by the requirement returned from `fn`.

```javascript
/**
 * @param {Function} fn
 * @return {Object}
 */
Array.prototype.groupBy = function(fn) {
    let obj = new Object()
    this.forEach((item) => {
        const key = fn(item)
        if (!obj[key]) {
            obj[key] = [];
        }
        obj[key].push(item);
    });
    return obj;
};

/**
 * [1,2,3].groupBy(String) // {"1":[1],"2":[2],"3":[3]}
 */
```

# 31. Join Two Arrays by ID
#### https://leetcode.com/problems/join-two-arrays-by-id/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 2.5 hrs

This problem asks to join two arrays by ID and it has to be in ascending order. 

The problem works as follows:
- An empty result array
- Add `arr1` to the result
- Add `arr1` to the result key by key if that id already exist, else just add it normally

Overall, this function joins 2 arrays into one and overrides values. 

```javascript
/**
 * @param {Array} arr1
 * @param {Array} arr2
 * @return {Array}
 */
var join = function(arr1, arr2) {
    const result=[]
    arr1.forEach((item)=>{
        result[item.id]=item;
    })
    arr2.forEach((item)=>{
        if (result[item.id]){
            for(const key in item) result[item.id][key] = item[key]
        } else {
            result[item.id]=item;
        }
    })
    return Object.values(result);
};
```