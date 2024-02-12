# 17. Reverse Vowels of a String
#### https://leetcode.com/problems/reverse-vowels-of-a-string/
### Level: Easy
### Study Plan: LeetCode 75
### Time Taken: 45 mins

This problem asks to reverse the vowels in a string. First I thought it was swapping but after re-reading the question, I realized that the question ask for reversing the vowels. 

The code works as follows:

- A empty array `vowelList` that will be used to store the vowels in the string `s`
- A empty string `result` to store the result
- First for loop is to get all the vowels in `vowelList`, and second for loop is to pop out the vowels in `vowelList`. It will naturally in reverse order because how `pop()` works.
  
Overall, this solution used 2 for loops to get the vowels to reverse in a string. It used very little memory (beats 99.70%) and a decent performance on the runtime (beats 51.91%). 

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U']
        vowelList = []
        result = ""
        for i in s:
            if i in vowels:
                vowelList.append(i)
        for i in s:
            if i in vowels:
                i = vowelList.pop()
            result += i
        return result
```

# 18. Can Place Flowers
#### https://leetcode.com/problems/can-place-flowers/
### Level: Easy
### Study Plan: LeetCode 75
### Time Taken: 1 hr

This problem asked if we can plant `n` plants in the `flowerbed`. The limitation is that the flowers cannot be planted in adjacent plots. Instead of using a basic for loop which I cannot iterate like `flowerbed[i]`, I used a while loop.

The code works as follows:

- An empty `canPlant` integer to be added when it can plant
- If the left and right plot and the current plot are empty, we will plant a flower and add 1 to `canPlant`
- When the left and right are the edges, it will be considered as empty too. 
  
Overall, this problem is tricky because it tested many test cases. This problem has an acceptance rate of 30%. I also submitted multiple rejected submissions because the edge cases were not in the test cases. 

```python
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        canPlant = 0
        i = 0
        while i != len(flowerbed):
            if (i == 0 or flowerbed[i-1] == 0) and flowerbed[i] == 0 and (i == len(flowerbed)-1 or flowerbed[i+1] == 0):
                canPlant += 1
                flowerbed[i] = 1
            i += 1
        return canPlant >=n
```

# 19. Cache With Time Limit
#### https://leetcode.com/problems/cache-with-time-limit/
### Level: Medium
### Study Plan: 30 Days of JavaScript
### Time Taken: 3.5 hrs  

This problem asks for the cache with a time limit. I used `setTimeout()` and `clearTimeout()` in the set function. I am not the most familiar with the prototype so I had to learn that myself. I had difficulty understanding where to store the key and getting the timer. I had to get help from ChatGBT to understand that I was storing the key in the wrong place with the wrong constructor. 

The code works as follows:

- Set empty object in the main function.
- In the set function, store key, value, and timer in the empty cache.
- If the previous key exists, then clear time out.
- Set timer to delete cache.
- In the get function, get the key value, else get -1.
In the count function, get the length of the keys.

Overall, this object `TimeLimitedCache` sets cache and multiple helper functions to set, get, and count the cache. When the different value for the same key is entered, the cache duration will refresh. 

```javascript
var TimeLimitedCache = function() {
    this.cache = {};
};

/** 
 * @param {number} key
 * @param {number} value
 * @param {number} duration time until expiration in ms
 * @return {boolean} if un-expired key already existed
 */
TimeLimitedCache.prototype.set = function(key, value, duration) {
    const keyExist = this.cache[key];
    if (keyExist) {
        clearTimeout(keyExist.timer);
    }
    const timer = setTimeout(() => {
        delete this.cache[key];
    }, duration);
    this.cache[key] = { value, timer };
    return Boolean(keyExist);
};

/** 
 * @param {number} key
 * @return {number} value associated with key
 */
TimeLimitedCache.prototype.get = function(key) {
    return this.cache[key] ? this.cache[key].value : -1;
};

/** 
 * @return {number} count of non-expired keys
 */
TimeLimitedCache.prototype.count = function() {
    return Object.keys(this.cache).length;
};
```