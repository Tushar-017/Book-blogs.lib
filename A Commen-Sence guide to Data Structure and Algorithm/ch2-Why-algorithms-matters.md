### Although the word algorithm sounds like something complex, it really isn't

- An algorithm is simply a set of instructions for completing a task.

- To explore new algorithms we need to explore one new DS:

### Order Arrays

- You guessed it - an array where values are always in order
  Ex - [3, 17, 18, 202]
- ##### Array operations
- **Read** - lookup can take just 1 step via index
- **Search** -
  - linear search - stop if found the value or the value is greater than the search item (left to right)
  - _Binary Search_
- **Insert** -
  - step1: Find(search) the right place to put the value in the order
  - step2: shift and make a room
  - step3: insert the value.

- **Delete** - Which index: (remove and shift to close the gap)
  1. delete last index - 1 step (best case)
  2. delete somewhere at the middle or beginning - (N(shift) + 1) steps - O(N)

##### Binary Search

- step1: First, establish the upper and the lower bound. (generally first and the last element of the order array)
- step2: start a loop keep a check lower_bound <= upper bound
- step3: calculate the mid point of lower-upper
- step4: compare the the search value with mid_point.( ===, < or >)
- return null if not found until the loop ends

##### Binary Search VS Linear Search

with an array containing 100 value

- Linear search: 100 steps
- Binary search: 7 steps (to calculate the steps for binary search think it like how many time you have to divide the array by to ultimately get 1)

**NOTE:**

- _Keep in mind. Insertion in ordered arrays is slower than in standard arrays. But have much faster search(binary search)_
