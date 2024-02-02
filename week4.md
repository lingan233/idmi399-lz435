# 11. Combination Sum
#### https://leetcode.com/problems/combination-sum/
### Level: Medium
### Study Plan: Top 100 Liked
### Time Taken: 4 hrs

This problem asks for all unique combinations of `candidates`. Although I learned backtracking in week 2 of the course, I still need to relearn it because I still don’t have a super strong foundation with that.

The code works as follows:

- Implements a depth-first search (dfs) function that has an end case of when `target == 0`.
- Instead using an additional variable called sum or total, `target` is being edited to get the combinations when `target` equal to 0.
- If `target` is negative or if the index `i` runs outside of the length of the candidates, then the branch ends. 
- While it is searching, the value of `candidates[i]` will be minus from `target` to be tested to see if it will equal 0.
- When index 1 is finished, then it will move the index 2 to see if there is any possible combination

In this method `combinationSum`, the function has a recursive function built inside called `dfs` that will call itself until all the possible unique combination is found. 

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:    
        combinations = []

        def dfs(i, current, target):
            if target <= 0:
                if target == 0:
                    combinations.append(current.copy())
                return
            
            if i < len(candidates):
                current.append(candidates[i])
                dfs(i, current, target - candidates[i])
                current.pop()
                dfs(i+1, current, target)

        dfs(0, [], target)
        print(combinations)
        return combinations

```
# 12. Add Two Promises
#### https://leetcode.com/problems/add-two-promises/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 2 hrs

This problem introduced a new concept for me. I have seen async and await functions before but I am not the most familiar. I also never heard of promise before this problem. Therefore, I went and learned the basic concept of promises. I use the `.then()` to get the value and added them together. After I submit my result, there are many different types of solutions. Some are more simple than others but less efficient. There are many other related methods and concepts that I didn’t have a chance to understand further.

The code works as follows:
- Returns promise resolve and reject
- When `promise1` get its value then it waits for `promise2` get its value
- When all get its value then we return it as resolved with the sum of each value. 


```javascript
/**
 * @param {Promise} promise1
 * @param {Promise} promise2
 * @return {Promise}
 */
var addTwoPromises = async function(promise1, promise2) {
    return new Promise((resolve, reject) => {
        promise1.then((value1)=>{
            promise2.then((value2)=>{
                return resolve(value1+value2);
            })
        })
    });
};

/**
 * addTwoPromises(Promise.resolve(2), Promise.resolve(2))
 *   .then(console.log); // 4
 */
```

# 13. Sleep
#### https://leetcode.com/problems/sleep/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken:  30 mins

I used a `setTimeuot()` method to set the timeout as the input. The problem itself is simplistic. I had a question about my memory use because the other solution taking very few memory looks very similar to mine. 

```javascript
/**
 * @param {number} millis
 * @return {Promise}
 */
async function sleep(millis) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve();
        }, millis);
    });
}

/** 
 * let t = Date.now()
 * sleep(100).then(() => console.log(Date.now() - t)) // 100
 */
```

