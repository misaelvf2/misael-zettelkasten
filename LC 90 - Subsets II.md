# LC 90 - Subsets II
202210021545
Difficulty: <mark style="background: #FFB86CA6;">Medium</mark>

## Problem Statement
>Given an integer array `nums` that may contain duplicates, return _all possible subsets (the power set)_.
>
>The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

This problem is very similar to [[LC 78 - Subsets]]. The only difference is that this time, the input array may contain duplicate elements. 

The solution will follow a very similar outline to the one in [[LC 78 - Subsets]], with some subtle changes to guarantee that the solution set does not contain duplicates.

There are two general approaches to guaranteeing that the solution does not contain duplicates. 

## Approach #1 - Keep track of seen solutions with a set

The first approach, which is not very elegant, but easier to come up with, is to realize that, if we had a set or some sort of [[Hashmap|hashmap]], we could verify whether a solution is a duplicate in constant time. The catch is that lists are not hashable objects, and thus cannot serve as the keys to such a hashmap.

To get around this limitation, we need to come up with a scheme to convert lists into a hashable object. One such scheme involves transforming a list into a sorted string, and then using the sorted string representation as keys to a hashmap.

For example, if one of our subsets were $[2, 1]$, we would first sort the subset into $[1, 2]$, convert it into the string "1, 2", then store the string in a hashmap. The next time that we encounter a duplicate subset--for example, $[1, 2]$, it would get converted into the string "1, 2", and keyed into the hashmap, at which point we would realize that it is a duplicate solution, and skip adding it to our result.

We could also sort the input as a first step in the algorithm. This guarantees that all the strings will be sorted, and is also more efficient, as the sorting only happens once, as opposed to at every leaf node. 

```python
def subsets(nums):
	result = []
	seen = set()
	nums.sort()  # This helps us to detect duplicate solutions

	def search(k, subset):
		# Base case
		if k == len(nums):
			subset_str = convert_to_string(subset)
			if subset_str in seen:
				result.append(subset[:])
				seen.add(subset_str)
			return
		# Recursive case
		# Choice: Don't include element
		search(k + 1, subset)
		# Choice: Do include element
		subset.append(nums[k])
		search(k + 1, subset)
		# Backtrack
		subset.pop()

	search(0, [])
	return result

def convert_to_string(subset):
	return ",".join([str(elem) for elem in subset])
```

### Time Complexity
We need to enumerate all possible subsets. If there were no duplicate elements, then we could form $2^n$ such subsets. Each time we generate a subset, we must perform a deep-copy operation to the result list. This is a $O(n)$ operation.

Additionally, we perform a sorting operation at the beginning. This will take $O(n \times log\ n)$. 

Taken together, the time complexity is $O(n \times 2^n)$. 

> [!INFO]
> This is a loose upper bound. As the input array may contain duplicates, the true number of unique subsets may be smaller than $2^n$.

### Space Complexity
We need to keep track of all solutions. We previously established that a loose upper bound on the true number of unique solutions is $O(2^n)$. Each solution will contain at most $O(n)$ elements. Therefore, the space complexity is $O(n \times 2^n)$. 

## Approach #2 - Prune the search tree
The more elegant, although slightly less intuitive, approach is to prune the search tree by skipping over duplicate elements as we encounter them in the search tree.

The way this works is, when faced with the choice of either including or not including an element, if we choose *not* to include, then we look ahead to the elements to the right, and skip over any duplicate instances of the element we are choosing not to include.

For instance, suppose our input is $A = [1, 2, 2, 3]$. When the search tree is at index $1$, we must make a choice to either include or not include the element at index $1$, namely, $A[1] = 2$. If we choose *not* to include $A[1] = 2$, we must make sure to also skip any duplicate instances of $2$. 

Notice that we are assuming that the input is sorted. This is not a given. So as a first step in the algorithm, we must sort the elements to facilitate skipping over duplicates.

```python
def subsets(nums):
	result = []
	nums.sort()

	def search(k, subset):
		# Base case
		if k == len(nums):
			result.append(subset[:])
			return
		# Recursive case
		# Choice: Don't include element, nor its duplicates
		i = k
		while i < len(nums) - 1 and nums[i + 1] == nums[i]:
			i += 1
		search(i + 1, subset)
		# Choice: Do include element
		subset.append(nums[k])
		search(k + 1, subset)
		# Backtrack
		subset.pop()

	search(0, [])
	return result
```

### Time Complexity
As before, the time complexity is $O(n \times 2^n)$. Note again that this is a loose upper bound; because we are applying an optimization that prunes the search tree, the search tree may be a lot smaller. However, characterizing and quantifying this effect is somewhat involved.

### Space Complexity
As before, the space complexity is $O(n \times 2^n)$. 

#Algorithms 
#ProgrammingInterviews 
#LeetCode
#LCMedium
#Backtracking

