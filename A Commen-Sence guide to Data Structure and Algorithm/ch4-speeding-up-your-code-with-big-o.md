# Chapter 4 Quick Notes: Speeding Up Your Code With Big-O

## What I learned

1. I saw Bubble Sort in action and understood how it repeatedly compares and swaps adjacent values.
2. I reviewed its efficiency and why it is considered a quadratic-time algorithm in typical use.
3. I transformed one quadratic-time problem into a linear-time solution.

## Key memory points

- Bubble Sort is useful for learning, but not great for large datasets.
- Big-O thinking helps me spot slow patterns early.
- Reworking logic can reduce runtime dramatically, for example from $O(n^2)$ to $O(n)$.

## One-line takeaway

The main win in this chapter was learning to recognize a slow $O(n^2)$ approach and redesign it into a faster $O(n)$ solution.

## Code examples

### 1) Bubble Sort (learning version)

```python
def bubble_sort(arr):
	n = len(arr)
	for end in range(n - 1, 0, -1):
		swapped = False
		for i in range(end):
			if arr[i] > arr[i + 1]:
				arr[i], arr[i + 1] = arr[i + 1], arr[i]
				swapped = True
		if not swapped:
			break
	return arr
```

### 2) Quadratic approach: check duplicates

```python
def has_duplicate_quadratic(arr):
	for i in range(len(arr)):
		for j in range(i + 1, len(arr)):
			if arr[i] == arr[j]:
				return True
	return False
```

### 3) Linear approach: optimize with a set

```python
def has_duplicate_linear(arr):
	seen = set()
	for value in arr:
		if value in seen:
			return True
		seen.add(value)
	return False
```

### Time complexity reminder

- Bubble Sort: worst and average case $O(n^2)$
- Duplicate check (nested loops): $O(n^2)$
- Duplicate check (set-based): $O(n)$ average
