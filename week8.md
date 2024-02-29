# 24. Reverse Words in a String
#### https://leetcode.com/problems/reverse-words-in-a-string/
### Level: Medium
### Study Plan: Leetcode 75
### Time Taken: 2 hrs

This problem ask to reverse the words in a string and delete all the non-functional space. I took a long time creating a bad and complicated solution. After I submit the solution, I found a simpler solution that is only one line and more efficient. 

```python 
class Solution:
    def reverseWords(self, s: str) -> str:
        result = []
        word = ""
        for index, i in enumerate(s):
            if i == " " and word != "":
                result.insert(0, word);
                word = ""
            elif i != " ":
                word += i
                if index == len(s)-1:
                    result.insert(0, word);
        return ' '.join(result);
```

```python 
class Solution:
    def reverseWords(self, s: str) -> str:
        return ' '.join(s.split()[::-1])
```



# 25. Product of Array Except Self
#### https://leetcode.com/problems/product-of-array-except-self/
### Level: Medium
### Study Plan: Leetcode 75
### Time Taken: 4 hrs

This problem asks for the product of the array except itself without division. This problem hinted for people to use the left product and right product to solve it. The algorithm is difficult to understand. I had to get help using a YouTube video teaching this problem.
The problem works as follows:
- Calculate the prefix and store it in the result array.
- Prefix is calculated by multiplying `nums[i]` and prefix is stored in `result[]` before prefix for the current `num[i]` is calculated.
- Same thing for postfix but in reverse order. 
  
Overall, the function `productExceptSelf` returns the result of prefix multiplied by postfix.

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)
        prefix = 1
        postfix = 1
        for i in range(len(nums)):
            result[i] = prefix
            prefix *= nums[i]
        for i in range(len(nums)-1, -1, -1):
            result[i] *= postfix
            postfix *= nums[i]
        return result
```
# 26. Increasing Triplet Subsequence
#### https://leetcode.com/problems/increasing-triplet-subsequence/
### Level: Medium
### Study Plan: Leetcode 75
### Time Taken: 2 hrs
This problem ask for triplet that is in an increasing order. The problem also didn’t specify that the triplet could be not consecutive. I started with basic `nums[i]`, `nums[i-1]`, `nums[i-2]`. Those has a issue with index become negative and also only considering consecutives. I had trouble figuring out the right algorithm. I watched someone else’s video discussing how the algorithm should work and wrote my own code for it. 

The problem works as follows:
- `i` is the min and `j` is the max
- `i` increase as `x` the current value runs
- `j` decrease as `x` runs
- When `x` is bigger than `j`, meaning `i>j>x`, there is an increasing triplet

Overall, the function `increasingTriplet` returns true or false based on if it contains an increasing triplet.

```python
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        i = max(nums)
        j = max(nums)

        for x in nums:
            # if x is smallest then i = x
            if x < i:
                i = x
            # if j is smaller than max and larger than min then j = x
            if x <= j and x > i:
                j = x
            # if x is larger than j then return 1
            if x > j:
                return 1
        return 0
```