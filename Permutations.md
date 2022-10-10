# Permutations
202210042038

In combinatorics, a permutation represents a reordering of elements from a set. For example, given a set $A = \{3, 1, 2\}$, a permutation of $A$ is $\{2, 1, 3\}$. This set has $3 \times 2 \times 1 = 6$ possible permutations. 

In contrast to [[Combinations|combinations]], order *does* matter in permutations.

## Algorithm - Permutations with $n$ distinct elements
```python
def permutations(nums):
	result = []

	def search(perm, chosen):
		# Base case
		if len(perm) == len(nums):
			result.append(perm[:])
			return
		# Recursive case
		# Iterate through all choices,
		# skipping previously chosen elements
		for i, num in enumerate(perm):
			if chosen[i]:
				continue
			perm.append(num)
			chosen[i] = 1
			search(perm, chosen)
			# Backtrack
			perm.pop()
			chosen[i] = 0

	chosen = [0] * len(nums)
	search([], chosen)
	return result
```

## Algorithm - Permutations with duplicate elements
```python
def permutations(nums):
	result = []
	nums.sort()

	def search(perm, chosen):
		# Base case
		if len(perm) == len(nums):
			result.append(perm[:])
			return
		# Recursive case
		# Iterate through all choices,
		# skipping previously chosen elements,
		# and avoiding duplicate solutions
		prev = None
		for i, num in enumerate(nums):
			if chosen[i] or num == prev:
				continue
			perm.append(num)
			chosen[i] = 1
			search(perm, chosen)
			# Backtrack
			perm.pop()
			chosen[i] = 0
			prev = num

	chosen = [0] * len(nums)
	search([], chosen)
	return result
```

#Backtracking 
#Algorithms 