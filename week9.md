# 27. Permutations
#### https://leetcode.com/problems/permutations/
### Level: Medium
### Study Plan: Top 100 Liked
### Time Taken: 3 hrs

This problem asks for simple permutation. I remember permutation from a few weeks ago, but to actually solving the problem is difficult. I first try to write seudo code describing how I think the program should work.

```python
# for num in nums
    # add 1
    # run permutation again
        # add 2
            # run permutation again
                # add 3
                # append to result
```

I wasn’t able to solve the problem myself, but I think my seudo code was somewhat on the right track. I used some help from Youtube to solve the problem after I couldn’t figure it out. 

The problem works as follows:

- Base case when there is only 1 num in nums
- Return result array and the copy of nums - will be equal to `perms` in the outer function
- Run the for loop for the length of nums
- Pop the first index and add it back on after permutation is done
- Depth-first search by recursion
    - Perms first equal the last int in the nums
    - It appends the second last int
    - Go back to the previous node and create another branch
    - Continue until there is only 1 num in nums
    - Return `result`

Overall, the problem wants a simple permutation. The function permute uses recursion to call itself multiple times to achieve permutation. 

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result = []
        
        if len(nums) == 1:
            return [nums[:]]

        for i in range(len(nums)):
            n = nums.pop(0)
            perms = self.permute(nums)
            for x in perms:
                x.append(n)
            result.extend(perms)
            nums.append(n)

        return result
```

# 28. N-Queens
#### https://leetcode.com/problems/n-queens/
### Level: Hard
### Study Plan: Top 100 Liked
### Time Taken: 4 hrs

This problem asks to solve for n queens in a n by n chess board. Queens cannot attack each other. I understood the big idea of this solution and wrote some seudo code.

```python
    # check the horizontal/vertical/diagnal
    # move queens around

    # for n times
        # put down a queen
        # if the new queen not in the way of the old queen
            # call itself
                # store this result if n time is reached and queens not in the way of each other
                # else backtrack
```

However, I still lack the ability to solve this all by myself. I am still weak on combination, permutation, and backtrack. Youtube has helped me out on solving this problem.

The problem works as follow:

- Because queen cannot be seen on horizontal, vertical, and diagonal, col set represent vertical, posDiag and negDiag each represent diagonal in one direction
- Base case is when row equals to n
- Backtrack adds the queen and add all the numbers that represent this specific queen in the sets we set up earlier, delete those after we backtrack.
- If queen is in column or diagonal then skips

Overall, this problem solves the famous N-Queen puzzle by using backtrack. 

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        col = set()
        posDiag = set()
        negDiag = set()
        result = []
        board = [["."] * n for i in range(n)]
        def backtrack(r):
            if r == n:
                result.append(["".join(row) for row in board])
                return 
            
            for c in range(n):
                if c in col or (r + c) in posDiag or (r - c) in negDiag:
                    continue # this skips this turn

                col.add(c)
                posDiag.add(r + c)
                negDiag.add(r - c)
                board[r][c] = "Q"

                backtrack(r + 1)

                col.remove(c)
                posDiag.remove(r + c)
                negDiag.remove(r - c)
                board[r][c] = "."
        backtrack(0)
        return result
```