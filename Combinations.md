# Combinations

In combinatorics, a combination represents a selection of elements chosen from a set of elements, such that the order of the elements does not matter. This is in contrast to [[Permutations|permutations]], wherein the order does matter.

Suppose we have a set of $n$ elements $S$. We can form a $k$-combination of $S$ by selecting $k$ elements from $S$ in any order. 

When dealing with combinations, we often specify whether repetition is allowed. That is, can we repeatedly choose the same element from $S$ in forming our $k$-combination?

#TODO Write more details on numbers of combinations for the case with and without repetition.

## Algorithm - k-combinations with repetition

```python
def combinations(nums, k):
	result = []

	def search(start, combo):
		# Base case
		if len(combo) == k:
			result.append(combo[:])
		# Recursive case
		else:
			# Iterate through all choices,
			# taking care to avoid duplicate combinations
			for i in range(start, len(nums)):
				combo.append(nums[i])
				search(i, combo)
				# Backtrack
				combo.pop()
	search(0, [])
	return result
```

#Backtracking 
#Algorithms 