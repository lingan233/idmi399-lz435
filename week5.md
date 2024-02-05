# 14.Timeout Cancellation
#### https://leetcode.com/problems/timeout-cancellation/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 1 hr

I have used the `setTimeout()` function, but I have never used the `clearTimeout()` function. The description of the problem is confusing for me. I have to re-read the description multiple times. The problem description asked for a return of `cancelFn`. The function `cancellable` passes in 3 parameters: `fn`, `args`, and `t`. 

The code works as follows:

- A `cancelFn` function to cancel the timeout. 
- A `timer` function to set the timeout using the parameters passed in. 
- Return `cancelFn`

Overall, this program delay the execution of the function `fn` by t milliseconds. `cancelFn` is called with `cancelTimeMs` outside of my code. If cancelFn is canceled before the timer finished then it will be canceled and vise versa. 

```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function(fn, args, t) {
    const cancelFn = function(){
        clearTimeout(timer);
    }
    const timer = setTimeout(() => {
        fn(...args);
    }, t);

    return cancelFn;
};

/**
 *  const result = [];
 *
 *  const fn = (x) => x * 5;
 *  const args = [2], t = 20, cancelTimeMs = 50;
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
 *  const maxT = Math.max(t, cancelTimeMs);
 *           
 *  setTimeout(cancel, cancelTimeMs);
 *
 *  setTimeout(() => {
 *      console.log(result); // [{"time":20,"returned":10}]
 *  }, maxT + 15)
 */
```

# 15. Promise Time Limit
#### https://leetcode.com/problems/promise-time-limit/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 2 hrs

This problem is similar the last problem as it also uses the `setTimeout()` function and promises. After submitting my solution and viewing other people’s solutions, I found the method `Promise.race()` might be better for this problem. I will look into `Promise.race()` more in future questions. Besides that, I also find areas that I could improve and make more efficient on my code so I improved my code after the first submission. 

My code works as follows:

- Returns a promise that resolve and reject
- A `setTimeout()` to reject when the time limit is exceeded
- Try and catch error for running the function with arguments.

Overall, this problem adds error handling the requirement with the other requirement `t` being a determining factor for if the promise should be rejected. 

```javascript 
/** first try
 * @param {Function} fn
 * @param {number} t
 * @return {Function}
 */
var timeLimit = function(fn, t) {
    
    return async function(...args) {
       return new Promise(async(resolve, reject) => {
            try{
                setTimeout(() => {
                    reject("Time Limit Exceeded");
                }, t);
                const result = await fn(...args);
                resolve(result);
            }catch(error){
                reject(error);
            }
        }); 

        // fn(...params).then(resolve).catch(reject)
    }
};

/**
 * const limited = timeLimit((t) => new Promise(res => setTimeout(res, t)), 100);
 * limited(150).catch(console.log) // "Time Limit Exceeded" at t=100ms
 */
```

```javascript 
/** second try
 * @param {Function} fn
 * @param {number} t
 * @return {Function}
 */
var timeLimit = function(fn, t) {
    return async function(...args) {
       return new Promise((resolve, reject) => {
            setTimeout(() => {
                reject("Time Limit Exceeded");
            }, t);
            fn(...args).then(resolve).catch(reject);
        }); 
    }
};

/**
 * const limited = timeLimit((t) => new Promise(res => setTimeout(res, t)), 100);
 * limited(150).catch(console.log) // "Time Limit Exceeded" at t=100ms
 */
```

# 16. Kids With the Greatest Number of Candies
#### https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/
### Level: Easy
### Study Plan: LeetCode 75
### Time Taken: 30 mins

This problem asks for if each item inside an array is the greatest number inside the array when each item is added by a number called `extraCandies`. 

The code works as follows:

- `result[]` to store the answer.
- `max(candies)` to find the max inside the array of number
- `append(1)` or `append(0)` to represent true or false
  
Overall, this is a simple problem that compares if the total number larger than the original max number of candies. It will return the array of true and false to represent if each item has the greatest number of candies. 

```python
class Solution:
    def kidsWithCandies(self, candies: List[int], extraCandies: int) -> List[bool]:
        result = []
        for i in candies:
            total = i + extraCandies   
            if total >= max(candies):
                result.append(1)
            else:
                result.append(0)
        return result
```