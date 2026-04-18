# Chapter 2: Why Algorithms Matter

An algorithm is simply a set of instructions to complete a task.

The better the algorithm, the fewer steps your program needs.

---

## Ordered Arrays

An ordered array keeps values sorted at all times.

Example: `[3, 17, 18, 202]`

### Operations

| Operation       | How it works                                                         | Typical cost |
| --------------- | -------------------------------------------------------------------- | ------------ |
| Read            | Access by index                                                      | `O(1)`       |
| Search (linear) | Move left to right until found (or value becomes larger than target) | `O(N)`       |
| Search (binary) | Repeatedly split range in half                                       | `O(log N)`   |
| Insert          | Find correct position, shift elements, insert                        | `O(N)`       |
| Delete          | Remove value and shift elements to close gap                         | `O(N)`       |

---

## Binary Search (Step-by-Step)

Use binary search only when data is sorted.

1. Set `lower_bound` to the first index and `upper_bound` to the last index.
2. While `lower_bound <= upper_bound`, keep searching.
3. Compute `mid = (lower_bound + upper_bound) / 2`.
4. Compare target with `mid` value:
   - If equal, return `mid`.
   - If target is smaller, move `upper_bound` left.
   - If target is larger, move `lower_bound` right.
5. If loop ends, target is not present (return `null` or `-1`).

---

## Binary Search vs Linear Search

For an array with 100 values:

- Linear search: up to 100 steps
- Binary search: about 7 steps

That difference grows as data grows.

> Trade-off: ordered arrays usually have slower insertion, but much faster search.
