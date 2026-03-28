### The organization of data does't just matter for organizational sake, but can significantly impact how fast your code run.

- Array & Set (appear same but)
- O -> Big O! Notation.

**NOTE:**

- _Measure Speed of an operation : Speed in terms of step not as per the time. Because the time can change as per the quality of the hardware._

### Array: The foundational DS

- Whenever a computer allocates an array. It also make a note at which memory address the array begins. (memory address and index are different concept.)
- technical jargon
  - size of the Array -> n
  - index of an array -> (0- (n-1) range)

- ##### Array operations
- **Read** - lookup can take just 1 step via index
- **Search** - lookup every cell until find the value - linear search[O(N) - steps](alt efficient algos)
- **Insert** - At where: (add and shit shift)
  1. inserting an element at end - 1 step (best case)
  2. inserting somewhere at the middle or beginning - (N + 1) steps - O(N) (worst case)

- **Delete** - Which index: (remove and shift to close the gap)
  1. delete last index - 1 step (best case)
  2. delete somewhere at the middle or beginning - (N(shift) + 1) steps - O(N)

**NOTE:**

- _Fact about computer - computer has immediate access to all the memory address but have no idea about what value they store before hand._

### Sets: how single rule can affect the efficiency

A set is a DS(just like array in this case) that does not allow duplicates within it.

- ##### Set operations
- **Read** - lookup can take just 1 step via index(\*_same as array_)
- **Search** - lookup every cell until find the value - linear search[O(N) - steps](alt efficient algos)(\*_same as array_)
- **Insert** - At where: (add and shit shift)
  <ins>1st step</ins> -> _Search_ the array(N steps) for not already present value, then following:
  1. inserting an element at end - 1 step (best case)
  2. inserting somewhere at the middle or beginning - (2N + 1) steps - O(N) (worst case)

- **Delete** - Which index: (remove and shift to close the gap)(\*_same as array_)
  1. delete last index - 1 step (best case)
  2. delete somewhere at the middle or beginning - (N(shift) + 1) steps - O(N)
