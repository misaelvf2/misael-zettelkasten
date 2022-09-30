# LC 46 - Permutations
202209300028

Difficulty:  <mark style="background: #FFB86CA6;">Medium</mark>

## Problem: Given an array of $n$ distinct integers, return all possible permutations of the array

A permutation is a reordering of elements. Suppose we have a list of integers $[1, 2, 3]$. The following are all the permutations of this list:

- $[1, 2, 3]$
- $[1, 3, 2]$
- $[2, 1, 3]$
- $[2, 3, 1]$
- $[3, 1, 2]$
- $[3, 2, 1]$

The following intuition helps us understand how to derive permutations: at every step, we must choose one out of all remaining elements. For the first step, we have $n$ possible choices, since none of the elements have yet been chosen. In the second step, we have $n - 1$ possible choices, as we can no longer choose the previously chosen element. This goes on until we can no longer choose any more elements.

Therefore, the total number of permutations will be $n \times n - 1 \times \cdots 1 = n!$ 

## Solution
This problem is most easily solved by using a recursive approach. To see the recursive nature of the problem, notice that we can represent the problem using a decision tree, with each node representing an index into the input list, and the edges representing a choice of the next element to choose.

Suppose our input list is $nums = [1, 2, 3]$. 

At the root node, we have the index 0. At this point, no elements have yet been chosen to be in the permutation. Thus, we have three edges coming out of the root node, one for each potential choice.

Following the first edge represents choosing $1$ as our first element, the second edge represents a choice of $2$, and so on. The next level down in the tree will consist of three nodes for the index 1. At this point, we have 2 choices remaining, and so can only have 2 edges coming out of each of the three nodes. We continue this process until have run out of possible choices, thus arriving at the leaf nodes. Once at the leaf node, we have a complete permutation, which we add to our list of permutations.

This solution follows the [[Backtracking|backtracking]] approach.

We will also need a bit vector to keep track of the elements that have already been chosen. As we go down the tree, we add the chosen element to our permutation (which represents a partial candidate solution), set its corresponding bit, and recurse. To backtrack, simply pop the elements from the list, and clear the corresponding bit.

```python
def permutations(nums):
    result = []
    chosen = [False] * len(nums)
    permutation = []

	def permutation_aux():
		# Base case
		if len(permutation) == len(nums):
			result.append(permutation[:])
			return
		# Recursive case
		# Iterate through all choices
		for i, num in enumerate(nums):
			# Element already chosen
			if chosen[i]:
				continue
			# Element not yet chosen
			permutation.append(num)
			chosen[i] = True
			permutation_aux()
			# Backtrack
			permutation.pop()
			chosen[i] = False
	permutation_aux()
	return result
```

### Time Complexity
There are $n!$ permutations. We need to enumerate all of them, as well as keep track of them in our result list. Copying each permutation to the result list takes time $O(n)$. Therefore, the time complexity is $O(n \times n!)$.

### Space Complexity
Similar reasoning follows for space complexity. We need to keep track of each permutation. There are $n!$ of them, each of size $n$. Therefore, the space complexity is also $O(n \times n!)$. 

### Notes
As we know, every recursive algorithm can be changed to an iterative algorithm. However, the iterative algorithm may be much harder and less intuitive to implement. Therefore, for this problem, we will assume that the recursive approach is good enough.

#Algorithms 
#ProgrammingInterviews 
#LeetCode
#LCMedium
#Backtracking 