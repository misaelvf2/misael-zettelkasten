
# Generating Subsets
202209251850

## Problem: Given a set S with n elements, generate all the subsets of S

Suppose we are given a set of numbers $A = \{0, 1, 2\}$. We are asked to generate (or enumerate) all the subsets of $A$. In mathematical terms, this is also known as the power set of $A$, denoted $P(A)$. Here, $P(A) = \{\{\}, \{0\}, \{1\}, \{2\}, \{0, 1\}, \{0, 2\}, \{1, 2\}, \{0, 1, 2\}\}$.

The powerset of any arbitrary set $S$ will always contain $2^n$ elements, where n is the number of elements in $S$. This is because, when constructing a subset of $S$, we have 2 options for every element: we may either include it, or we may not include it.

It is often helpful to think of this problem in terms of the binary numbers. We can define a mapping from subsets to binary numbers as follows:
$\{\}$ -> 0b0
$\{0\}$ -> 0b1
$\{1\}$ -> 0b10
$\{2\}$ -> 0b11
$\{0, 1, 2\}$ -> 0b111

---

This problem may either be solved recursively or iteratively.

## Recursive Approach
In this approach, imagine we have a binary tree, starting with the $0th$ element as the root node.
At every step, we have the choice of either including the ith element in our subset, or **not** including it in the subset.

This approach is also called [[Backtracking|backtracking]].

![[Pasted image 20220925191135.png]]

```python
def generate_subsets(nums):
    n = len(nums)
    subsets = []
    def aux_generate_subsets(k):
        # Base case
        if n == k:
            subsets.append(subset.copy())
        # Recursive case
        else:
            # Don't include in subset
            aux_generate_subsets(k + 1)
            subset.append(nums[k])
            # Include in subset
            aux_generate_subsets(k + 1)
            subset.pop()
    subset = []
    aux_generate_subsets(0)
    return subsets
```

### Time Complexity
The powerset of a set $S$ contains $2^n$ subsets. We need to enumerate all such subsets. Therefore, the time complexity is $O(2^n)$.

### Space Complexity
There are a couple of things to consider for the space complexity. For one thing, we are storing the list of subsets in a variable $subsets$. We already know that there will be $2^n$ such subsets, so the list will grow to a size $O(2^n)$. We also need to consider the recursive nature of the algorithm. The call graph will generate a binary tree; this tree will have a maximum depth of $n$. Therefore, we will need to allocate $O(n)$ space in the stack.

Therefore, the space complexity is $O(2^n)$. 

> [!INFO]
> We are assuming that the problem asks us to *return* all the subsets. If we are merely asked to print them, then there is no need to maintain the list of subsets, and the space complexity is determined solely by the need to allocate space in the stack.

## Iterative Approach
The iterative approach is based on the mapping of subsets to binary numbers. It generates each subset by counting binary numbers starting from 0 to $2^n - 1$. For each generated subset, we need to map back to the original representation by iterating over the bits and determining whether an element is included in the subset or not, by testing whether the corresponding bit is set to 1. 

Testing whether a particular bit is set to 1 is a straightforward [[Bit Operations|bit operation]]: we simply take our reference binary number, and perform a bit-wise AND operation with the binary number corresponding to the position of the bit we want to test.

For example:
B = 0b1101
To determine if the 2th bit position is set, perform 0b1101 AND 0b100 = 0b1000 $!=$ 0; therefore, the 2th bit is indeed set.

```python
def generate_subsets(nums):
    n = len(nums)
    subsets = []
    for i in range(1 << n):
        subset = []
        for j in range(n):
            if i & (1 << j):
                subset.append(j)
        subsets.append(subset)
    return subsets
```
### Time Complexity
We still need to generate all $2^n$ subsets, so the time complexity remains unchanged at $O(2^n)$.

### Space Complexity
As before, we are assuming that the problem asks us to maintain and return a list of all the subsets. This list will grow to a size of $O(2^n)$, therefore the space complexity is also $O(2^n)$. However, if instead we are simply asked to print out the subsets, then we only need $O(n)$ space to store the currently-generated subset.

In any case, because we are generating every single subset, this problem falls under the general category of problems known as [[Complete Search|complete search]] problems.

#Algorithms 
#ProgrammingInterviews 
#Backtracking
#BitOperations