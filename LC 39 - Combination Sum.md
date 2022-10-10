# LC 39 - Combination Sum
202210011523

Difficulty: <mark style="background: #FFB86CA6;">Medium</mark>

## Problem: Given an array of unique integers and a target value, return all unique combinations of candidates whose sum is equal to the target value. 

A [[Combinations|combination]] represents a way of choosing among some elements. In contrast to permutations, the ordering of the chosen elements does not matter; the only thing that matters is which elements were chosen. 

When working with combinations, we usually given a parameter $k$ that represents the number of elements that we can choose from among the candidate elements. We are also told whether we can repeatedly choose elements or not.

For this particular problem, we are not directly given a parameter $k$. Instead, we must construct combinations such that the sum of all the chosen numbers is equal to a target value. Additionally, repetitions are allowed.

## Solution
Similarly to other [[Backtracking|backtracking]] problems, a decision tree helps us to reason about the problem and derive intuition.

In this decision tree, the nodes represent a candidate solution in the form of a combination and a combination sum. The edges from each node represents the choices that we can make. In the general case, we have $n$ possible choices. When we make a choice, we add it to our combination, and update the combination sum. When the combination sum is equal to the target, we have found a complete solution. This represents a base case. When the combination sum exceeds the target, then we know that we can abandon the branch.
To backtrack, we remove the current choice from the combination, and subtract it from the combination sum. We can do this either explicitly or implicitly.

The tricky part about this problem is knowing how to avoid repeated solutions. Remember, the problem asks us for all **unique** combinations, and order does not matter in a combination. So $[1, 1, 2$] is equal to $[1, 2, 1$], as combinations are concerned. The first approach we might come up with is to enumerate all solutions, even the repeated ones, and to filter out the repeated ones at the end. However, this is compuationally expensive. The other approach we might think of is to use some sort of set or hashmap to only store unique solutions. This, too, will not work, as lists are not hashable and thus cannot serve as the keys in a hashmap. We could come up with some kind of scheme to make the combinations unique and hashable, perhaps by representing the combination as a sorted string. This could work, but it is a little awkward.

Instead, the trick to avoiding repeated solutions is to realize that, because order does not matter in combinations, branches to the left of the current branch are guaranteed to have found all possible combinations that include elements preceding the current choice.

```python
def combination_sum(candidates, target):
	result = []

	def dfs(combo_sum, combo, start):
		# Base case
		if combo_sum == target:
			result.append(combo[:])
			return
		# Recursive case
		# Iterate through all choices
		for i in range(start, len(candidates)):
			if combo_sum + candidates[i] <= target:
				combo.append(candidates[i])
				dfs(combo_sum + candidates[i], combo, i)
				# Backtrack
				combo.pop()
	dfs(0, [], 0)
	return result
```

### Time Complexity
In general, we can approximate the time complexity of recursive algorithms as $O(branches^{depth})$. Here, $branches$ is loosely bound by $O(N)$, while depth is bound by $T/M$, where $T$ is the target value, and $M$ is the minimum element in the candidates array. Putting it all together, we have a loose upper bound of $O(N^{T/M})$ . Note that this analysis does not try to approximate the total number of solution combinations, but rather the total number of nodes in the resulting call graph. This analysis also ignores the time taken to make a deep copy of each solution, as this is only performed by the leaf nodes, which is a small proportion of all nodes in the tree.

### Space Complexity
We analyze the space complexity in terms of the space that must be allocated on the stack as we go deeper down the recursion tree. As established earlier, the depth of the tree will be bound by the number of times that we can add up the minimum number in the candidates until reaching or exeeding the target. Therefore, the space complexity is $O(T/M)$. 

This analysis also ignores the space used to store the results list, as that would entail trying to approximate the number of solution combinations, which is not straightforward.


#Algorithms 
#ProgrammingInterviews 
#LeetCode 
#LCMedium 
#Backtracking 