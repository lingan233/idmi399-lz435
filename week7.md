# 20. Interval Cancellation
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 1 hr

This problem asks for interval cancellation. At first, the problem was confusing because I didn’t know there is a `setInterval()` method in javascript. I attempted to solve the problem by `setTimeout()`. Because the description for this problem is confusing, I spend the most amount of time trying to understanding the problem. 

The problem works as follows:
- Run `fn` at the beginning
- Set an interval to run `fn` every `t` seconds
- Return a `cancelFn` to clear the interval

Overall, this var `cancellable` returns a cancel function and runs a `fn` for `t` interval. 

```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function(fn, args, t) {
    fn(...args);
    const interval = setInterval(() => {
        fn(...args);
    }, t);

    const cancelFn = () => clearInterval(interval);

    return cancelFn;
};

/**
 *  const result = [];
 *
 *  const fn = (x) => x * 2;
 *  const args = [4], t = 35, cancelTimeMs = 190;
 *
 *  const start = performance.now();
 *
 *  const log = (...argsArr) => {
 *      const diff = Math.floor(performance.now() - start);
 *      result.push({"time": diff, "returned": fn(...argsArr)});
 *  }
 *       
 *  const cancel = cancellable(log, args, t);
 *
 *  setTimeout(cancel, cancelTimeMs);
 *   
 *  setTimeout(() => {
 *      console.log(result); // [
 *                           //     {"time":0,"returned":8},
 *                           //     {"time":35,"returned":8},
 *                           //     {"time":70,"returned":8},
 *                           //     {"time":105,"returned":8},
 *                           //     {"time":140,"returned":8},
 *                           //     {"time":175,"returned":8}
 *                           // ]
 *  }, cancelTimeMs + t + 15)    
 */
```
# 21. Debounce
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 1 hr

This problem asks for a debounced version of `fn`. I didn’t know what debounce is, but I took some time to learn it. Debounce is a helpful concept to use in real life. 

The problem works as follow:

- Return a function that clear timeout for the `setTimeout` and run `setTimeout()`

Overall, this problem takes `fn` and `t` and debounce the `fn` based on `t`.

```javascript
/**
 * @param {Function} fn
 * @param {number} t milliseconds
 * @return {Function}
 */
var debounce = function(fn, t) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => {
            fn(...args);
        }, t);
    }
};

/**
 * const log = debounce(console.log, 100);
 * log('Hello'); // cancelled
 * log('Hello'); // cancelled
 * log('Hello'); // Logged at t=100ms
 */
```

# 22. Is Object Empty
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 30 mins

This problem asks if the object is empty. Because this problem is under Json in the study plan, I first tried to stringify the length of the `obj`. This is not the best approach because it is not the most efficient. I then took the most common solution for this problem.

```javascript
/**
 * @param {Object|Array} obj
 * @return {boolean}
 */
var isEmpty = function(obj) {
    return Object.keys(obj).length === 0
};
```
# 23.Sort By
### Level: Easy
### Plan: 30 Days of JavaScript
### Time Taken: 30 mins

This problem asks to sort in ascending order after applying `fn`.  I used built in function `sort()` and added `fn` inside the `sort()`. 

```javascript
/**
 * @param {Array} arr
 * @param {Function} fn
 * @return {Array}
 */
var sortBy = function(arr, fn) {
    return arr.sort((a, b) => fn(a) - fn(b));
};
```