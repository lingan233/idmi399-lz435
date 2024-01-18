# 4. Function Composition
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 1 hr 15 mins

This question asked about function composition. I am not familiar with the concept of function composition so I tried to learn it through googling. Function composition is a way to call functions consecutively. It is very similar to pipe except that their order of calling function is different. Pipe calls left to right where as the compose calls right to left. I also then learned that a good way to do compose and pipe is through reduce() and reduceRight(). I was able to use reduceRight() in the solution to achieve compose. 

Here is some explanation of reduce() cited from this helpful website: 

https://builtin.com/software-engineering-perspectives/javascript-reduce

JavaScript reduce() is a higher order function used in data manipulation that reduces an array to a single value. It takes two parameters: an accumulator and the current element of an array. Its uses include calculating the sum or product of all elements, finding the maximum and minimum value, flattening an array, and more.

I first wrote a more beginner level code by creating a function called fn that takes the accumulator and return the f(accumulator). Then I wrote a shorthanded version for it. Although I was able to solve that problem but this problem is confusing for me to understand why accumulator is on the left and function on the right when the compose function itself runs from right to left.


    /**
    * @param {Function[]} functions
    * @return {Function}
    */
    var compose = function(functions) {
        return function(x) {
            return functions.reduceRight((acc, f) => f(acc), x);
        }
    };

    // var compose = function(functions) {
    //     function fn(accumulator, f) {
    //         return f(accumulator);
    //     }
    //     return function(x) {
    //         return functions.reduceRight(fn, x);
    //     }
    // };

    /**
    * const fn = compose([x => x + 1, x => 2 * x])
    * fn(4) // 9
    */

# 5. Return Length of Arguments Passed
#### https://leetcode.com/problems/return-length-of-arguments-passed/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 15 mins
This problem asked about the length of the passing arguments. To solve that, I just return the length of the argument. I already know there is a .length function in javascript, so the solution is intuitive. 

    /**
    * @param {...(null|boolean|number|string|Array|Object)} args
    * @return {number}
    */
    var argumentsLength = function(...args) {
        return args.length;
    };

    /**
    * argumentsLength(1, 2, 3); // 3
    */

# 6. Generate Parentheses
#### https://leetcode.com/problems/generate-parentheses/
### Level: Medium
### Study Plan: Top 100 Liked
### Time Taken: 3 hrs
This problem is another question under the backtracking topic. Although I self-taught backtracking myself on the last Top 100 Liked problem. It is still not very intuitive in how to solve this issue. I did end up searching for Youtube videos to explain the algorithm. 

This program essentially wants there to be all the combinations of n pairs of parentheses. To achieve that, the base case will be reached when the n pairs of parentheses are added. The program uses a recursive approach. When one branch completes its work and append a result, the previous stack get pop so that it can go through with a new branch. 

    class Solution:
        def generateParenthesis(self, n: int) -> List[str]:
            result = []
            stack = []
            def backtrack(openN, closeN):
                if openN == closeN == n:
                    result.append("".join(stack))
                    return
                if openN < n:
                    stack.append("(")
                    backtrack(openN+1, closeN)
                    stack.pop()
                if closeN < openN:
                    stack.append(")")
                    backtrack(openN, closeN+1)
                    stack.pop()
            backtrack(0,0)
            return result

# 7. Allow One Function Call
#### https://leetcode.com/problems/allow-one-function-call/
### Level: Easy
### Study Plan: 30 Days of JavaScript
### Time Taken: 1 hr
This problem wants a function to be only called once and after that, it wants to return undefined. In order to do that, we used a variable called isCalled to represent where or not it has been called. I learned about that … is spread syntax after having errors on the return fn(args). Then, I added the … which I wasn’t sure the specific definition before. 

    /**
    * @param {Function} fn
    * @return {Function}
    */
    var once = function(fn) {
        isCalled = false;
        return function(...args){
            if (isCalled){
                return undefined;
            }
            isCalled = true;
            return fn(...args);
        }
    };

    /**
    * let fn = (a,b,c) => (a + b + c)
    * let onceFn = once(fn)
    *
    * onceFn(1,2,3); // 6
    * onceFn(2,3,6); // returns undefined without calling fn
    */
