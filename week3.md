# 8. Memoize
#### https://leetcode.com/problems/memoize/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 2 hr

This javascript question asked about caching the values. The function memoize(fn) takes in a function and decides whether or not to call the fn. I thought about it needs an if-else for the cache. I was not sure how I should store the cache. I know that I could do localStorage, but a simple cached indexed array might be more efficient. 
I passed all 3 tests but when I submitted the solution, I only passed 19/20 of the tests. When “[[0,0],[0,0],[]]” is passed in, my code with run the fn twice. It is because I used the following code. 
```javascript
if (cache[key]) {
    return cache[key];
}
```
Therefore, the `cache[key]` is 0 when the input is `[[0,0],[0,0],[]]`, and the if statement will not run. I could use the `key` in cache instead of `cache[key]`. 

This code works as follows:
- Empty cache is set up as an indexed array `const cache` to take the `key` as index to find the stored value
`const key` is set up by stringifying the passing `args`
- If `key` exists in `cache`, then return the `cache`
- If not, then run the function to get the value in `cache` and return it

So the function memoize takes function with args as input and when the same arg is passed in, it will not call the function again. Instead, it will return the cached value. 


```javascript
/**
 * @param {Function} fn
 * @return {Function}
 */
function memoize(fn) {
    const cache = {}
    return function(...args) {
        const key = JSON.stringify(args);
        if (key in cache) {
            return cache[key];
        }
        return cache[key] = fn(...args);
    }
}


/** 
 * let callCount = 0;
 * const memoizedFn = memoize(function (a, b) {
 *	 callCount += 1;
 *   return a + b;
 * })
 * memoizedFn(2, 3) // 5
 * memoizedFn(2, 3) // 5
 * console.log(callCount) // 1 
 */
```

# 9. Merge Strings Alternately
#### https://leetcode.com/problems/merge-strings-alternately/
### Level: Easy
### Study Plan: LeetCode 75
### Time Taken: 1 hr

This problem wants to manipulate strings so that `word1` and `word2` can mix and match their characters. I wanted to do a for loop so I googled how to do a for loop with 2 items. Then i zipped the word1 and word2 to do the for loop. 

In this problem, the code works as follows:

- The empty string `merged` is created to store the merged result
- The for loop adds `char1` and `char2` in order 
- After the shorter word ended, the rest of the longer is added to the `merged` in the 2 if statement.
- 
So the function merges words alternately and when the shorter word ended, the rest of the longer word will be added to the merged.

```python 3
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        merged = ""
        for char1, char2 in zip(word1, word2):
            merged += char1
            merged += char2
        if len(word1) > len(word2):
            merged += word1[len(word2):]
        if len(word2) > len(word1):
            merged += word2[len(word1):]
        return merged
```


# 10. Greatest Common Divisor of Strings
#### https://leetcode.com/problems/greatest-common-divisor-of-strings/
### Level: Easy
### Study Plan: LeetCode 75
### Time Taken: 3 hrs

This problem might be more appropriately categorized as medium because if not using the `math.gcd` method, then it is complicated to implement and get the greatest common strings. I did not know that method so I did a manual method. 

The code works as follows:

- The `gcdOfStrings` is a recursive method that takes `str1` and `str2` and find the gcd.
- The first if statement make sure that `str1` is always longer or equal to `str2`
- The second if statement is a base case for returning the gcd
- The third if statement is a base case for there being no gcd
- The last line does the recursion. It takes a greedy approach to run the method `gcdOfStrings` to see if `str2` matches the sliced `str1` at the right side at the length of `str2`.
  
So this function takes a recursive approach to slice strings and compare them to find the greatest common divisor.

```python 3
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        if len(str2) > len(str1):
            str1, str2 = str2, str1
        if str2 == str1: 
            return str1
        if str1[:len(str2)] != str2:
            return ""
        return self.gcdOfStrings(str1[len(str2):], str2)
```