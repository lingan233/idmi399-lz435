# 1. Counter
#### https://leetcode.com/problems/counter/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 45 mins

First, I wanted to just return  n=n+1, but it turns out that it returns n+1, n+2, n+3 and we want it to return n, n+1, n+2. 

Then, I was thinking about using an if-else statement. I was trying to add a count variable and have that count++ when it is called. However, it still doesn’t work because I realized that I can’t count++ after the return and I could potentially have a n and a count or maybe a variable called isItFirstTime. However, these don’t seem efficient and the best way to do it. 

It took me a while to get to the solution of creating a variable inside the return function so that the currentCount will be assigned to count a call later. I was able to increment a variable after something was returned with a workaround. The currentCount captures the value of the count before it is incremented every time. 

After I submitted the solution that I thought was good, I realized that the best solution was just to return n++. I thought n=n+1 is the same as n++, but it is not. Returning n++ is returning n and then adding 1. Always those simple and stupid mistakes as always. Returning n++ probably has the shortest runtime and takes the minimal memory. So I submitted it again but I don’t know why my runtime and memory are worse than my first submission. I guess it didn’t change that much, but it is definitely better practice to do the simpler solution. 

```javascript
/**
* @param {number} n
* @return {Function} counter
*/
var createCounter = function(n) {

    return function() {
        return n++;
    };

};

/** 
* const counter = createCounter(10)
* counter() // 10
* counter() // 11
* counter() // 12
*/
```


# 2. Counter II
#### https://leetcode.com/problems/counter-ii/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 20 mins           

This question was similar to the last question. I know how to increment, decrement, and reset. I just forgot about how to add that function inside this createCounter function. I looked online and find how this would work. Seems like people put it in a return. After I submitted the solution, I realized that some people still create the function inside this function and then return the function name only in the return. 

```javascript
/**
* @param {integer} init
* @return { increment: Function, decrement: Function, reset: Function }
*/
var createCounter = function(init) {
let value = init;
return {
    increment: function(){
    value += 1;
    return value;
    },
    decrement: function(){
    value -= 1;
    return value;
    },
    reset: function(){
    value = init;
    return value;
    }
} 
};

/**
* const counter = createCounter(5)
* counter.increment(); // 6
* counter.reset(); // 5
* counter.decrement(); // 4
*/
```

# 3. Letter Combinations of a Phone Number
#### https://leetcode.com/problems/letter-combinations-of-a-phone-number/
### Level: Medium
### Study Plan: Top 100 Liked
### Time Taken: 4 hrs

This problem is more difficult than the previous two questions. I started with a dictionary/mapping for converting number to letters. Then I realized that I need to remember the previous number’s letters in the for loop to continue mapping it. So I went to study backtracking. 

I watched YouTube videos on backtracking and it is somehow related to permutation and recursion. I used some help from chatGBT to explain the pseudo code of permutation, etc. I also used chatGBT to debug. I was using permutation then I realized that combination is better for this case, so I changed to combination. Permutation and combination are similar and both uses backtracking. The only difference between the two is that combination doesn’t produce replicates in different order. 

To change permutation into combination, the previous number is skipped in the next loop like “12, 13; 23” instead of “12, 13; 21, 23; 31, 32” where every number no matter if it has been run will run again. 

This program uses numbers as input to generate letter combinations. Each number is converted into an array of letters, then the letters use combination, backtracking, and recursion to produce an array of results as letter combinations. Detailed comments on the solution code explain what I did in the code. 

```python 3
class Solution:

    def letterCombinations(self, digits: str) -> List[str]:
        letter = {
            "2": ["a", "b", "c"],
            "3": ["d", "e", "f"],
            "4": ["g", "h", "i"],
            "5": ["j", "k", "l"],
            "6": ["m", "n", "o"],
            "7": ["p", "q", "r", "s"],
            "8": ["t", "u", "v"],
            "9": ["w", "x", "y", "z"]            
        }

        def combine(current_combination, start):
            if start == len(digits): # this is when it ends
                result.append("".join(current_combination)) # this joins array values into a string
                return 
                
            # for loop of the individual letter of the letters of the index of digits. 
            # input "23"; digits[0] = 2; letter[digits[0]] = ["a", "b", "c"]; char = "a"
            for char in letter[digits[start]]: 
                current_combination.append(char) 
                # printing current_combination after appending looks something like this: 
                # ['a'] ['a', 'd'] ['a', 'e'] ['a', 'f']

                combine(current_combination, start + 1) # recursion into the next loop
                current_combination.pop() # backtracking

        result = []
        if digits: # if there is inputs
            combine([], 0)

        return result # return empty array if there is no input                        
```
    