# Chapter 5: Quick Notes - Optimize Code With and Without Big O

## Selection Sort vs Bubble Sort

**Key Insight:** Selection sort is more efficient than bubble sort, but both are O(n²).

- **Bubble Sort**: Compares adjacent elements and swaps them if they're in wrong order. In worst case, swaps happen many times per pass.
- **Selection Sort**: Finds the minimum element and places it in correct position. Fewer swaps overall.

**Why Selection Sort is Better:** Even though both are O(n²), selection sort performs significantly fewer swaps in practice. Bubble sort can swap n times per pass, while selection sort swaps only once per pass.

**Real-world Impact:** For an array of 100 elements, bubble sort could do ~5,000 swaps, while selection sort does only ~100 swaps. This matters in actual performance, even though Big O notation doesn't capture it.

---

## Why We Ignore Constants in Big O

**The Rule:** In Big O notation, we drop constant multipliers and focus only on the dominant term.

**Example:**

- Selection sort: O(n² / 2) → simplified to O(n²)
- An algorithm doing 2n + 100 operations → simplified to O(n)

**Why?**

1. **As data grows, constants become negligible.** With n = 1,000,000, dividing by 2 doesn't matter compared to the squaring effect.
2. **Big O measures scalability, not raw speed.** It tells us how algorithm performance degrades as input grows, not absolute execution time.
3. **Different hardware/languages affect constants anyway.** An algorithm with constant 2 on one machine might have constant 3 on another, so exact constants are less relevant.

**Bottom Line:** Big O focuses on the _shape_ of growth (linear, quadratic, exponential) rather than fine details, making it a universal language for comparing algorithm efficiency.
