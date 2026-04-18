## Oh Yes! Big O notation

- **Time complexity of Big O** - It has nothing to do with how much time a particular algorithm going to take.
- **Big O of N** - deals with how much steps(N steps etc.) a particular algorithm take

#### If there are N data elements how many steps an algorithm going to take?

### O(1)- Constant Time (fastest)

- Big O of N literally say it has no dependency on the N data elements

#### The sole reason of Big O is how the algorithm will perform when the data grows

### O(N) - eg. - linear search

- number of steps are directly proportional to the N data elements

- _O(100) is more efficient O(N)_

### O(log N) - eg. - Binary search

**LOGARITHM**

- Q. What is log anyway?
- A. A log is an inverse of exponential

- 2^3 = 2 _ 2 _ 2
- log 8 => 8/2 => 4/2 => 2/2 => 1 (log2 8 means how many times you have to divide it by two to get 1)

| N Elements | O(1) | O(N)      | O(log N) |
| ---------- | ---- | --------- | -------- |
| 10         | 1    | 10        | 3        |
| 100        | 1    | 100       | 7        |
| 1,000      | 1    | 1,000     | 10       |
| 10,000     | 1    | 10,000    | 13       |
| 100,000    | 1    | 100,000   | 17       |
| 1,000,000  | 1    | 1,000,000 | 20       |

_With Big O Notation, we have a consistent system which alow us to compare two algorithms_
