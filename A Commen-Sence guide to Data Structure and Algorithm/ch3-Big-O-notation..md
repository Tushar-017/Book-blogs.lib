# Chapter 3: Big O Notation

Big O does not measure exact clock time.

It measures how the number of **steps** grows as input size `N` grows.

> Main question: if there are `N` data elements, how many steps will the algorithm need?

---

## Why Big O Matters

Big O gives us a consistent way to compare algorithms as data scales.

Two algorithms might look similar on small input, but their growth can be very different on large input.

---

## Common Growth Rates

### `O(1)` - Constant Time

The number of steps does not depend on `N`.

### `O(N)` - Linear Time

The number of steps grows directly with `N`.

Example: linear search.

### `O(log N)` - Logarithmic Time

The search space is repeatedly cut in half.

Example: binary search.

---

## Quick Logarithm Intuition

Log is the inverse of exponentiation.

- `2^3 = 8`
- `log2(8) = 3`

Another way to think about `log2(8)`:

`8 -> 4 -> 2 -> 1` (divide by 2 three times)

---

## Step Comparison Table

| N elements | O(1) |      O(N) | O(log N) |
| ---------- | ---: | --------: | -------: |
| 10         |    1 |        10 |        3 |
| 100        |    1 |       100 |        7 |
| 1,000      |    1 |     1,000 |       10 |
| 10,000     |    1 |    10,000 |       13 |
| 100,000    |    1 |   100,000 |       17 |
| 1,000,000  |    1 | 1,000,000 |       20 |

As `N` grows, the gap becomes dramatic. That is why Big O is so useful.
