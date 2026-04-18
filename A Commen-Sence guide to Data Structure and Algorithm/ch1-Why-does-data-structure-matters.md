# Chapter 1: Why Data Structure Matters

How data is organized can dramatically change how fast your code runs.

Two structures can look similar, but behave very differently when reading, searching, inserting, or deleting data.

> We measure performance in **steps**, not clock time, because hardware speed can vary.

---

## Array: The Foundational Data Structure

When a computer allocates an array, it records the starting memory address.
That is why arrays support very fast index-based access.

- Array size: `n`
- Valid index range: `0` to `n - 1`

### Core Operations on Arrays

| Operation             | How it works                           | Typical cost |
| --------------------- | -------------------------------------- | ------------ |
| Read                  | Access by index                        | `O(1)`       |
| Search                | Check cells one by one (linear search) | `O(N)`       |
| Insert (end)          | Add to next free slot                  | `O(1)`       |
| Insert (middle/start) | Shift elements, then insert            | `O(N)`       |
| Delete (end)          | Remove last element                    | `O(1)`       |
| Delete (middle/start) | Delete and shift to close gap          | `O(N)`       |

> Computers can access memory addresses quickly, but they do not automatically know what value is stored where.

---

## Set: One Rule Changes the Cost

A set (in this context) is like an array, but it does **not** allow duplicates.

That single rule changes insertion behavior:

1. First, search to confirm the value is not already present.
2. Then insert (and shift if needed).

### Core Operations on Sets

| Operation             | How it works            | Typical cost |
| --------------------- | ----------------------- | ------------ |
| Read                  | Access by index         | `O(1)`       |
| Search                | Linear search           | `O(N)`       |
| Insert (end)          | Search + insert         | `O(N)`       |
| Insert (middle/start) | Search + shift + insert | `O(N)`       |
| Delete (end)          | Remove last element     | `O(1)`       |
| Delete (middle/start) | Delete and shift        | `O(N)`       |

In short, sets trade insertion speed for uniqueness guarantees.
