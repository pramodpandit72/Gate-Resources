# GATE CSE – Algorithms

> **Syllabus covered:** Searching, sorting, hashing; asymptotic worst-case time and space complexity; algorithm design techniques (greedy, dynamic programming, divide-and-conquer); graph traversals; minimum spanning trees; shortest paths.
>
> **Level:** GATE Computer Science and Information Technology (CS)
>
> **Language:** Simple English, with pseudocode and C-style examples where useful.

---

## Table of Contents

1. [Syllabus Checklist](#1-syllabus-checklist)
2. [Introduction to Algorithms](#2-introduction-to-algorithms)
3. [Asymptotic Time and Space Complexity](#3-asymptotic-time-and-space-complexity)
4. [Searching](#4-searching)
5. [Sorting](#5-sorting)
6. [Hashing](#6-hashing)
7. [Algorithm Design Techniques](#7-algorithm-design-techniques)
   - [Greedy Method](#71-greedy-method)
   - [Dynamic Programming](#72-dynamic-programming)
   - [Divide-and-Conquer](#73-divide-and-conquer)
8. [Graph Fundamentals and Traversals](#8-graph-fundamentals-and-traversals)
9. [Minimum Spanning Trees](#9-minimum-spanning-trees)
10. [Shortest-Path Algorithms](#10-shortest-path-algorithms)
11. [Important Complexity Summary](#11-important-complexity-summary)
12. [Common GATE Traps](#12-common-gate-traps)
13. [Quick Revision Notes](#13-quick-revision-notes)
14. [Practice Questions](#14-practice-questions)
15. [Detailed Answer Key](#15-detailed-answer-key)

---

# 1. Syllabus Checklist

Use this checklist to track your preparation.

- [ ] Meaning and properties of an algorithm
- [ ] Input size and operation counting
- [ ] Best, average and worst cases
- [ ] Big-O, Big-Omega and Big-Theta notation
- [ ] Order of growth and comparison of functions
- [ ] Worst-case time complexity
- [ ] Auxiliary space and recursion-stack space
- [ ] Linear search and binary search
- [ ] Bubble, selection and insertion sort
- [ ] Merge sort, quick sort and heap sort
- [ ] Counting sort, radix sort and bucket sort
- [ ] Stability, in-place sorting and comparison sorting
- [ ] Hash functions and collision handling
- [ ] Separate chaining and open addressing
- [ ] Linear probing, quadratic probing and double hashing
- [ ] Load factor and clustering
- [ ] Greedy choice and optimal substructure
- [ ] Activity selection and fractional knapsack
- [ ] Job sequencing and Huffman coding (greedy applications)
- [ ] Dynamic programming, memoization and tabulation
- [ ] 0/1 knapsack, LCS and matrix-chain multiplication
- [ ] Divide-and-conquer and recurrence relations
- [ ] Master theorem (for common divide-and-conquer recurrences)
- [ ] Graph representations and their complexities
- [ ] BFS and DFS
- [ ] Connected components, cycle detection and topological sorting
- [ ] Spanning trees and minimum spanning trees
- [ ] Kruskal's and Prim's algorithms
- [ ] Disjoint Set Union (Union-Find)
- [ ] Shortest paths: BFS, DAG relaxation, Dijkstra and Bellman-Ford
- [ ] All-pairs shortest paths: Floyd-Warshall

---

# 2. Introduction to Algorithms

## 2.1 What is an algorithm?

An **algorithm** is a finite sequence of clear steps used to solve a problem.

Example: To find the largest number in an array:

1. Assume the first element is the largest.
2. Visit every remaining element.
3. If the current element is larger, update the largest value.
4. After visiting all elements, return the largest value.

An algorithm is independent of a particular programming language. It can be written in plain English, pseudocode, a flowchart or a programming language.

## 2.2 Important properties

| Property | Meaning |
|---|---|
| Input | Takes zero or more well-defined inputs. |
| Output | Produces at least one result. |
| Definiteness | Every step must be clear and unambiguous. |
| Finiteness | Must finish after a finite number of steps. |
| Effectiveness | Each step must be basic enough to be carried out. |
| Correctness | Must produce the required result for every valid input. |

## 2.3 Correctness versus efficiency

- **Correctness:** Does the algorithm produce the right answer?
- **Time efficiency:** How does the amount of work grow with input size?
- **Space efficiency:** How much additional memory does it need?

An algorithm that is fast but gives incorrect answers is not a valid solution. First establish correctness, then analyze efficiency.

---

# 3. Asymptotic Time and Space Complexity

## 3.1 Why do we analyze complexity?

Suppose two algorithms solve the same problem. One takes roughly `n` steps and another takes roughly `n²` steps. For a small input, the difference may be minor. For a very large input, the second algorithm can require dramatically more work.

Complexity analysis studies how resource usage grows as input size grows. It allows us to compare algorithms without depending on a particular computer, processor speed or programming language.

## 3.2 Input size

Input size is represented by `n` in many problems.

Examples:

- Array algorithms: `n` is the number of elements.
- String algorithms: `n` is often the number of characters.
- Graph algorithms: use `V` for vertices and `E` for edges.
- Matrix algorithms: dimensions may be `m × n`.

Always identify the input-size variable before calculating complexity.

## 3.3 Time complexity

**Time complexity** describes how the number of basic operations grows with input size. It is not normally the exact number of seconds.

Example:

```c
for (int i = 0; i < n; i++) {
    printf("%d", i);
}
```

The loop executes `n` times, so its time complexity is:

\[
T(n) = \Theta(n)
\]

## 3.4 Best, average and worst cases

Consider linear search in an array of `n` elements.

| Case | Situation | Comparisons |
|---|---|---:|
| Best | Target is at the first position | 1 |
| Average | Target is typically somewhere in the array | Proportional to `n` under common assumptions |
| Worst | Target is at the last position or absent | `n` |

The **worst case** is the maximum work an algorithm can perform for any valid input of size `n`.

Unless a question asks for another case, carefully check whether it requests worst-case, average-case or expected complexity.

## 3.5 Asymptotic notations

Asymptotic notation describes growth for sufficiently large input sizes. Constant factors and lower-order terms are ignored.

### Big-O: upper bound

\[
f(n) = O(g(n))
\]

There exist positive constants `c` and `n₀` such that:

\[
0 \le f(n) \le c\,g(n), \quad n \ge n_0
\]

It says that `f` does not grow faster than a constant multiple of `g` for sufficiently large `n`.

### Big-Omega: lower bound

\[
f(n) = \Omega(g(n))
\]

There exist positive constants `c` and `n₀` such that:

\[
0 \le c\,g(n) \le f(n), \quad n \ge n_0
\]

It gives an asymptotic lower bound.

### Big-Theta: tight bound

\[
f(n) = \Theta(g(n))
\]

There exist positive constants `c_1`, `c_2` and `n₀` such that:

\[
0 \le c_1g(n) \le f(n) \le c_2g(n), \quad n \ge n_0
\]

It means that `f` and `g` grow at the same asymptotic rate.

### Important distinction

Big-O is an upper-bound notation; it is not automatically the same thing as worst-case complexity. We can express the worst-case running time using Big-O, Big-Theta or another appropriate bound. The case being analyzed and the notation used are two separate ideas.

For example, an algorithm may have worst-case time `Θ(n²)`. It is also correct to say that this is `O(n²)`, but `Θ(n²)` is tighter.

## 3.6 Common orders of growth

From slower growth to faster growth:

\[
1 < \log n < n < n\log n < n^2 < n^3 < 2^n < n!
\]

This ordering is for sufficiently large `n` (the logarithm base is irrelevant asymptotically).

| Complexity | Common name | Example |
|---|---|---|
| `O(1)` | Constant | Access an array element by index |
| `O(log n)` | Logarithmic | Binary search |
| `O(n)` | Linear | Linear search |
| `O(n log n)` | Linearithmic | Merge sort, heap sort |
| `O(n²)` | Quadratic | Basic bubble sort, selection sort |
| `O(n³)` | Cubic | Three nested loops over `n` values |
| `O(2ⁿ)` | Exponential | Basic recursive subset enumeration |
| `O(n!)` | Factorial | Enumerating all permutations |

## 3.7 How to calculate time complexity

### Rule 1: Consecutive statements

```c
statement1;  // O(1)
statement2;  // O(n)
statement3;  // O(n^2)
```

Total:

\[
O(1+n+n^2)=O(n^2)
\]

Keep the dominant term.

### Rule 2: A single loop

```c
for (int i = 0; i < n; i++) {
    // O(1) work
}
```

The body runs `n` times: `Θ(n)`.

### Rule 3: Nested loops

```c
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // O(1)
    }
}
```

The inner loop runs `n` times for each of `n` outer iterations:

\[
T(n)=n\times n=\Theta(n^2)
\]

### Rule 4: Triangular nested loop

```c
for (int i = 0; i < n; i++) {
    for (int j = 0; j <= i; j++) {
        // O(1)
    }
}
```

The total number of executions is:

\[
1+2+\cdots+n=\frac{n(n+1)}{2}=\Theta(n^2)
\]

### Rule 5: Multiplicative loop variable

```c
for (int i = 1; i < n; i *= 2) {
    // O(1)
}
```

After `k` iterations, `i = 2^k`. The loop stops when `2^k ≥ n`:

\[
k=\lceil\log_2 n\rceil
\]

Time complexity: `Θ(log n)`.

### Rule 6: Additive loop variable with a larger step

```c
for (int i = 0; i < n; i += 3) {
    // O(1)
}
```

There are approximately `n/3` iterations. Constant factors are ignored, so time is `Θ(n)`.

### Rule 7: Two independent loops

```c
for (int i = 0; i < n; i++) { /* ... */ }
for (int j = 0; j < n * n; j++) { /* ... */ }
```

Total: `n + n²`, so `Θ(n²)`, not `Θ(n³)`.

## 3.8 Space complexity

**Space complexity** measures memory usage as a function of input size.

It is useful to distinguish:

- **Input space:** Memory occupied by the input itself.
- **Auxiliary space:** Extra memory used by the algorithm, excluding the input (unless a question defines it differently).
- **Total space:** Input storage plus auxiliary storage.
- **Recursion stack:** Memory used by active recursive calls.

Example: Iterative linear search uses `O(1)` auxiliary space. It does not need an extra array.

Example: Merge sort on an array generally uses `O(n)` auxiliary array space, in addition to its recursion stack of `O(log n)` depth.

## 3.9 Recursion and space complexity

Each active recursive call may need a stack frame containing parameters, local variables and a return address.

| Recursion pattern | Maximum call depth | Stack space (assuming O(1) per frame) |
|---|---:|---:|
| `f(n-1)` until a base case | `O(n)` | `O(n)` |
| `f(n/2)` until a base case | `O(log n)` | `O(log n)` |
| Two recursive calls made one after another | Depends on deepest active branch | Not automatically `O(2^n)` stack space |

A recursive algorithm can take exponential time but use only linear stack space. Time and space must be analyzed separately.

## 3.10 Solved complexity examples

### Example 1

```c
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        count++;
    }
}
```

The inner body runs `1 + 2 + ... + n` times:

\[
\frac{n(n+1)}{2}=\Theta(n^2)
\]

**Answer:** `Θ(n²)` time, `Θ(1)` auxiliary space.

### Example 2

```c
int i = n;
while (i > 1) {
    i = i / 2;
}
```

The value is halved each time. The number of halvings is logarithmic.

**Answer:** `Θ(log n)` time, `Θ(1)` auxiliary space.

### Example 3

```c
for (int i = 1; i <= n; i *= 2) {
    for (int j = 0; j < n; j++) {
        work++;
    }
}
```

The outer loop runs `Θ(log n)` times and the inner loop runs `n` times per outer iteration.

**Answer:** `Θ(n log n)` time.

### Example 4: Nested loop with a changing bound

```c
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j *= 2) {
        work++;
    }
}
```

Outer loop: `n`; inner loop: `log₂ n`.

**Answer:** `Θ(n log n)` time.

---

# 4. Searching

Searching means finding whether a target value exists in a collection and, if it exists, locating its position.

## 4.1 Linear Search

### Idea

Check elements one by one from the beginning until the target is found or the array ends.

### Pseudocode

```text
LINEAR-SEARCH(A, n, key)
    for i = 0 to n - 1
        if A[i] == key
            return i
    return NOT-FOUND
```

### Dry run

Array: `[12, 7, 25, 9, 18]`, key: `9`.

| Comparison | Value | Result |
|---:|---:|---|
| 1 | 12 | Not equal |
| 2 | 7 | Not equal |
| 3 | 25 | Not equal |
| 4 | 9 | Found at index 3 |

### Complexity

| Case | Time |
|---|---:|
| Best | `Θ(1)` |
| Average | `Θ(n)` under common assumptions |
| Worst | `Θ(n)` |
| Auxiliary space | `Θ(1)` |

### Important points

- Works on sorted and unsorted collections.
- Simple and useful for small arrays.
- If the target is absent, all `n` elements are checked.

## 4.2 Binary Search

### Idea

Binary search works on a **sorted** array. It compares the target with the middle element and discards half of the remaining search range after each comparison.

### Iterative pseudocode

```text
BINARY-SEARCH(A, n, key)
    low = 0
    high = n - 1

    while low <= high
        mid = low + floor((high - low) / 2)

        if A[mid] == key
            return mid
        else if key < A[mid]
            high = mid - 1
        else
            low = mid + 1

    return NOT-FOUND
```

The expression `low + (high - low) / 2` avoids the possible overflow of `(low + high) / 2` in fixed-width integer languages.

### Dry run

Array: `[3, 8, 12, 17, 24, 31, 39, 45]`, key: `31`.

| Step | low | high | mid | A[mid] | Action |
|---:|---:|---:|---:|---:|---|
| 1 | 0 | 7 | 3 | 17 | Search right half |
| 2 | 4 | 7 | 5 | 31 | Found |

### Why is its time logarithmic?

After each iteration, the remaining interval is at most half its previous size.

After `k` iterations, its size is approximately:

\[
\frac{n}{2^k}
\]

The search ends when this is at most 1:

\[
\frac{n}{2^k}\leq 1 \Rightarrow k\geq\log_2 n
\]

Therefore, worst-case time is `Θ(log n)`.

### Complexity

| Version | Worst-case time | Auxiliary space |
|---|---:|---:|
| Iterative | `Θ(log n)` | `Θ(1)` |
| Recursive | `Θ(log n)` | `Θ(log n)` stack |

### Common mistakes

- Applying binary search to an unsorted array.
- Using `low < high` instead of `low <= high` without adjusting the algorithm appropriately.
- Updating `low = mid` or `high = mid` in a way that may cause an infinite loop.
- Forgetting that finding *any* occurrence is different from finding the first or last occurrence when duplicates exist.

## 4.3 First and last occurrence in a sorted array

When duplicates exist, ordinary binary search may return any matching position. To find the first occurrence:

1. When `A[mid] == key`, save `mid` as the current answer.
2. Continue searching the left half.

To find the last occurrence, save the answer and continue searching the right half.

Both take `O(log n)` time.

## 4.4 Linear search versus binary search

| Feature | Linear search | Binary search |
|---|---|---|
| Requires sorted data? | No | Yes |
| Worst-case time | `O(n)` | `O(log n)` |
| Iterative auxiliary space | `O(1)` | `O(1)` |
| Main operation | Check next element | Discard half the range |
| Suitable use | Small/unsorted data | Large sorted random-access data |

## 4.5 Solved example

A sorted array has 1,024 elements. At most how many halvings are required to reduce the search interval to one element?

\[
2^{10}=1024
\]

**Answer:** 10 halvings. Binary search also performs a final comparison to identify the candidate, depending on how the algorithm is counted. For GATE questions, follow the exact loop and comparison convention given.

---

# 5. Sorting

Sorting arranges data in a specified order, usually ascending or descending.

## 5.1 Important sorting terms

### Stable sorting

A sorting algorithm is **stable** if equal-key elements preserve their original relative order.

Example:

Input: `(A, 5), (B, 3), (C, 5)`

A stable ascending sort produces: `(B, 3), (A, 5), (C, 5)`.

`A` remains before `C` because both have key 5 and `A` appeared first.

### In-place sorting

An in-place algorithm uses only a small or constant amount of extra storage, under the convention used by the question. Some textbooks allow `O(log n)` stack space when describing an in-place sorting algorithm; always state whether recursion-stack space is counted.

### Adaptive sorting

An adaptive algorithm can perform less work when the input is already or nearly sorted. Insertion sort is a common example.

### Comparison-based sorting

The algorithm determines order using comparisons between keys. Merge sort, quick sort and heap sort are comparison sorts.

## 5.2 Sorting algorithms at a glance

| Algorithm | Best time | Average time | Worst time | Auxiliary space (typical implementation) | Stable? |
|---|---:|---:|---:|---:|---|
| Bubble sort (early stop) | `O(n)` | `O(n²)` | `O(n²)` | `O(1)` | Yes |
| Selection sort | `O(n²)` | `O(n²)` | `O(n²)` | `O(1)` | Usually no |
| Insertion sort | `O(n)` | `O(n²)` | `O(n²)` | `O(1)` | Yes |
| Merge sort (array) | `O(n log n)` | `O(n log n)` | `O(n log n)` | `O(n)` | Yes |
| Quick sort | `O(n log n)` | `O(n log n)` expected/typical | `O(n²)` | `O(log n)` expected stack; `O(n)` worst stack | Usually no |
| Heap sort | `O(n log n)` | `O(n log n)` | `O(n log n)` | `O(1)` iterative | No |
| Counting sort | `O(n+k)` | `O(n+k)` | `O(n+k)` | `O(n+k)` | Can be stable |
| Radix sort | `O(d(n+k))` | `O(d(n+k))` | `O(d(n+k))` | Depends on stable digit sort; often `O(n+k)` | Yes, with stable digit sort |

Here `k` is the key range or number of buckets for a digit pass, and `d` is the number of digit positions. These non-comparison sorts rely on assumptions about the keys.

## 5.3 Bubble Sort

### Idea

Compare adjacent elements and swap them if they are in the wrong order. After one full pass, the largest unsorted element reaches its final position at the end.

### Pseudocode

```text
BUBBLE-SORT(A, n)
    for i = 0 to n - 2
        swapped = false
        for j = 0 to n - 2 - i
            if A[j] > A[j + 1]
                swap(A[j], A[j + 1])
                swapped = true
        if swapped == false
            break
```

### Dry run

Input: `[5, 1, 4, 2]`.

- Pass 1: compare 5 and 1, swap; compare 5 and 4, swap; compare 5 and 2, swap → `[1, 4, 2, 5]`.
- Pass 2: compare 1 and 4; compare 4 and 2, swap → `[1, 2, 4, 5]`.
- Pass 3: no swap occurs, so the early-stop version terminates.

### Complexity and properties

- Worst-case time: `Θ(n²)`.
- Average time: `Θ(n²)`.
- Best time: `Θ(n)` with the `swapped` optimization.
- Auxiliary space: `Θ(1)`.
- Stable when only strictly out-of-order adjacent elements are swapped.

## 5.4 Selection Sort

### Idea

In each pass, find the minimum element in the unsorted part and place it at the beginning of that part.

### Pseudocode

```text
SELECTION-SORT(A, n)
    for i = 0 to n - 2
        minIndex = i
        for j = i + 1 to n - 1
            if A[j] < A[minIndex]
                minIndex = j
        swap(A[i], A[minIndex])
```

### Example

Input: `[29, 10, 14, 37, 13]`.

- Pass 1: minimum is 10 → `[10, 29, 14, 37, 13]`.
- Pass 2: minimum of the remaining part is 13 → `[10, 13, 14, 37, 29]`.
- Pass 3: minimum is 14 → no effective change.
- Pass 4: minimum is 29 → `[10, 13, 14, 29, 37]`.

### Complexity and properties

The number of comparisons is approximately:

\[
(n-1)+(n-2)+\cdots+1=\frac{n(n-1)}{2}
\]

So best, average and worst time are all `Θ(n²)`. Auxiliary space is `Θ(1)`. Standard selection sort is not stable because a swap can change the relative order of equal keys.

It performs only `O(n)` swaps, which can be useful when writes are expensive.

## 5.5 Insertion Sort

### Idea

Build a sorted portion from left to right. Take the next element and insert it into its correct position in the already sorted portion.

### Pseudocode

```text
INSERTION-SORT(A, n)
    for i = 1 to n - 1
        key = A[i]
        j = i - 1
        while j >= 0 and A[j] > key
            A[j + 1] = A[j]
            j = j - 1
        A[j + 1] = key
```

### Dry run

Input: `[5, 2, 4, 1]`.

- Insert 2 into `[5]` → `[2, 5, 4, 1]`.
- Insert 4 into `[2, 5]` → `[2, 4, 5, 1]`.
- Insert 1 into `[2, 4, 5]` → `[1, 2, 4, 5]`.

### Complexity and properties

| Case | Reason | Time |
|---|---|---:|
| Best | Already sorted; one comparison per new element | `Θ(n)` |
| Average | Many elements may need shifting | `Θ(n²)` |
| Worst | Reverse sorted; each new value shifts across the sorted part | `Θ(n²)` |

Auxiliary space: `Θ(1)`. Stable if equal elements are not shifted past one another (the condition uses `>` rather than `>=`). It is adaptive and useful for small or nearly sorted arrays.

## 5.6 Merge Sort

### Design technique: Divide-and-conquer

1. Divide the array into two halves.
2. Recursively sort each half.
3. Merge the two sorted halves.

### Pseudocode

```text
MERGE-SORT(A, left, right)
    if left >= right
        return
    mid = left + floor((right - left) / 2)
    MERGE-SORT(A, left, mid)
    MERGE-SORT(A, mid + 1, right)
    MERGE(A, left, mid, right)
```

`MERGE` compares the first unprocessed elements of the two sorted halves, copies the smaller one to a temporary array, and then copies any remaining elements.

### Dry run

Input: `[8, 3, 6, 2]`.

```text
             [8, 3, 6, 2]
              /        \
          [8, 3]       [6, 2]
           /  \         /  \
         [8]  [3]     [6]  [2]
           \  /         \  /
          [3, 8]        [2, 6]
              \        /
             [2, 3, 6, 8]
```

### Recurrence

Two subproblems of size `n/2` are solved, and merging takes linear time:

\[
T(n)=2T(n/2)+\Theta(n)
\]

By the Master theorem:

\[
T(n)=\Theta(n\log n)
\]

### Complexity and properties

- Best, average and worst time: `Θ(n log n)`.
- Auxiliary array space: `Θ(n)` for a typical array implementation.
- Recursion stack: `Θ(log n)`.
- Stable when the merge chooses the left item first on equal keys.
- Standard array merge sort is not in-place under the usual definition.

## 5.7 Quick Sort

### Design technique: Divide-and-conquer

Quick sort selects a **pivot**, partitions the array so that values smaller than the pivot are on one side and larger values are on the other, then recursively sorts the two sides.

### Pseudocode (conceptual)

```text
QUICK-SORT(A, low, high)
    if low < high
        p = PARTITION(A, low, high)
        QUICK-SORT(A, low, p - 1)
        QUICK-SORT(A, p + 1, high)
```

The exact partition procedure matters. Different partition schemes may return different pivot positions and comparison counts. In GATE questions, use the partition rule explicitly given.

### Best and worst partitions

- Best-like case: pivot divides the array into two nearly equal parts.
- Worst case: pivot is repeatedly the smallest or largest item, producing partitions of sizes `0` and `n-1`.

Balanced recurrence:

\[
T(n)=2T(n/2)+\Theta(n)=\Theta(n\log n)
\]

Worst recurrence:

\[
T(n)=T(n-1)+\Theta(n)=\Theta(n^2)
\]

### Complexity and properties

| Case | Time |
|---|---:|
| Best | `Θ(n log n)` |
| Expected with suitable randomized pivoting | `Θ(n log n)` |
| Worst | `Θ(n²)` |

Typical in-place partitioning uses `O(1)` extra array storage, but recursion stack space is `O(log n)` on balanced partitions and `O(n)` in the worst case. Standard quick sort is not stable.

Randomized pivot selection reduces the chance of consistently bad partitions; it does not remove the theoretical `O(n²)` worst case.

## 5.8 Heap Sort

### Idea

Use a binary heap. For ascending order:

1. Build a max heap.
2. Swap the root (maximum) with the last item in the heap.
3. Reduce the heap size by one.
4. Restore the max-heap property using heapify.
5. Repeat until one item remains.

A max heap has the largest key at its root. In an array representation with zero-based indexing:

- Parent of index `i`: `floor((i-1)/2)` for `i > 0`.
- Left child: `2i + 1`.
- Right child: `2i + 2`.

### Complexity

- Building a heap bottom-up: `Θ(n)`, not `Θ(n log n)`.
- Each extraction/heapify: `O(log n)`.
- `n` extractions: `O(n log n)`.
- Overall best, average and worst time: `Θ(n log n)`.
- Iterative array implementation auxiliary space: `Θ(1)`.
- Not stable in the standard implementation.

### Why is build-heap linear?

Most nodes are close to the leaves and require very little downward movement. The total work over all nodes is bounded by a geometric series and is `O(n)`. This is a frequently tested fact.

## 5.9 Counting Sort

Counting sort is a non-comparison sorting algorithm for keys in a reasonably small integer range.

### Idea

1. Count how many times each key occurs.
2. Convert counts into cumulative positions when stable output is required.
3. Place each input item into its correct output position.

If there are `n` elements and key values in a range of size `k`, time is `O(n+k)` and auxiliary space is `O(n+k)` for the stable output-array version.

Counting sort can be stable. To preserve stability, process the input from right to left when placing items using cumulative counts.

It is not automatically suitable when the key range is enormous compared with `n`.

## 5.10 Radix Sort

Radix sort processes keys one digit (or character position) at a time. A stable digit-sorting method is required to preserve the ordering established by earlier passes.

For `n` keys, `d` digit positions and a digit range of size `k`, a common LSD radix sort using counting sort takes:

\[
O(d(n+k))
\]

It is useful when keys have a bounded number of digits. The exact complexity depends on the digit representation and stable subroutine.

## 5.11 Bucket Sort

Bucket sort distributes values into buckets, sorts each bucket and concatenates them. Its expected time can be linear under assumptions such as values being distributed reasonably uniformly across a known range. Its worst case can be `O(n²)` if most items fall into one bucket and a quadratic-time bucket sort is used.

Do not claim linear worst-case time without stating the assumptions and the method used inside buckets.

## 5.12 Lower bound for comparison sorting

A comparison sort can be represented by a decision tree. It must distinguish among `n!` possible input permutations.

A binary decision tree with height `h` has at most `2^h` leaves, so:

\[
2^h \geq n!\Rightarrow h\geq\log_2(n!)=\Omega(n\log n)
\]

Therefore, any comparison-based sorting algorithm requires `Ω(n log n)` comparisons in the worst case.

This lower bound does not apply to non-comparison sorts such as counting sort when their key assumptions are satisfied.

## 5.13 Stability and in-place comparison

| Algorithm | Stable? | In-place? (typical implementation) |
|---|---|---|
| Bubble | Yes | Yes |
| Selection | No | Yes |
| Insertion | Yes | Yes |
| Merge | Yes | No for ordinary array implementation |
| Quick | No | Usually yes for partition array storage; stack is extra |
| Heap | No | Yes |
| Counting | Can be | No for standard stable output-array version |
| Radix | Yes if each digit pass is stable | Depends on digit sort |

---

# 6. Hashing

## 6.1 What is hashing?

Hashing stores and retrieves records using a **hash table**. A hash function converts a key into an array index.

\[
h(key)\rightarrow\{0,1,\ldots,m-1\}
\]

Here `m` is the table size.

Example: If `h(k) = k mod 10`, then key 47 maps to index 7.

## 6.2 Hash function

A good hash function should:

- Be deterministic: the same key should produce the same hash value.
- Be quick to compute.
- Distribute likely keys across the table reasonably evenly.
- Reduce collisions for the expected key set.

A hash function does not guarantee that different keys get different indices.

## 6.3 Collision

A **collision** occurs when two different keys map to the same table index.

Example:

\[
h(23)=23\bmod 10=3
\]

\[
h(43)=43\bmod 10=3
\]

Both keys map to index 3, so a collision occurs.

Collision resolution methods include separate chaining and open addressing.

## 6.4 Load factor

The load factor measures how full the hash table is.

\[
\alpha=\frac{n}{m}
\]

where `n` is the number of stored keys and `m` is the number of table slots.

For chaining, `α` can be greater than 1. For open addressing, the table must have an empty slot for insertion, so ordinarily `α < 1`.

## 6.5 Separate chaining

Each table index stores a collection (often a linked list) of keys that hash to that index.

Example with `h(k)=k mod 5`, inserting 12, 7, 22 and 9:

```text
Index 0:  --
Index 1:  --
Index 2:  12 -> 7 -> 22
Index 3:  --
Index 4:  9
```

(12, 7 and 22 all have remainder 2.)

### Complexity

- Expected search/insert/delete: `O(1 + α)` under uniform hashing assumptions.
- Worst case: `O(n)` if all keys land in one chain.
- Extra storage is used for links or collection nodes.

## 6.6 Open addressing

All keys are stored directly in the table. When a collision occurs, the algorithm probes other slots.

### Linear probing

\[
h_i(k)=(h(k)+i)\bmod m,\quad i=0,1,2,\ldots
\]

It checks the next slot, then the next, wrapping around at the end.

**Example:** Table size 7, `h(k)=k mod 7`, insert 10, 17, 24.

- 10 maps to 3 → place at index 3.
- 17 maps to 3 → index 3 occupied, try 4 → place at 4.
- 24 maps to 3 → indices 3 and 4 occupied, try 5 → place at 5.

Linear probing can cause **primary clustering**: long groups of occupied consecutive slots form and attract more keys.

### Quadratic probing

A common form is:

\[
h_i(k)=(h(k)+c_1i+c_2i^2)\bmod m
\]

The sequence of probe positions depends on the constants and table size. It reduces primary clustering but may have secondary clustering. It is not guaranteed to visit every table position for every choice of parameters.

### Double hashing

\[
h_i(k)=(h_1(k)+i\cdot h_2(k))\bmod m
\]

The second hash function determines the step size. For the probe sequence to cover the full table, the step size should be relatively prime to the table size. A common safe design with prime table size chooses a nonzero step smaller than the table size.

Double hashing generally reduces clustering compared with linear probing.

## 6.7 Clustering

| Type | Meaning | Commonly associated with |
|---|---|---|
| Primary clustering | Long contiguous occupied blocks develop | Linear probing |
| Secondary clustering | Keys with the same initial hash follow the same probe sequence | Quadratic probing |

## 6.8 Deletion in open addressing

Simply marking a deleted slot as empty can break a later search probe sequence. A search might stop at that empty slot even though the key is stored farther along the sequence.

A common solution is a **tombstone** (deleted marker). Search continues through tombstones, while insertion may reuse a tombstone when appropriate.

## 6.9 Hash table complexity

| Operation | Expected/common case | Worst case |
|---|---:|---:|
| Search | `O(1)` under good distribution and controlled load | `O(n)` |
| Insert | `O(1)` expected | `O(n)` (or failure if an open-addressed table is full) |
| Delete | `O(1)` expected | `O(n)` |

These are not unconditional guarantees. The expected performance relies on assumptions about the hash function, key distribution and load factor.

## 6.10 Solved hashing example

A hash table has size 11 and uses linear probing with `h(k)=k mod 11`. Insert `22, 33, 44, 55`.

- 22: `22 mod 11 = 0` → index 0.
- 33: maps to 0; index 0 occupied → index 1.
- 44: maps to 0; indices 0 and 1 occupied → index 2.
- 55: maps to 0; indices 0, 1 and 2 occupied → index 3.

Final occupied positions: 0, 1, 2 and 3 respectively.

---

# 7. Algorithm Design Techniques

A design technique is a general strategy for constructing an algorithm. The same problem may sometimes be solved using different techniques, but their correctness and complexity can differ.

## 7.1 Greedy Method

### 7.1.1 Basic idea

A greedy algorithm constructs a solution step by step. At each step it chooses the option that looks best according to a local rule, without reconsidering earlier choices.

A locally best choice does not always produce a globally optimal answer. A greedy strategy is valid only when the problem has the required structure and the choice rule can be justified.

### 7.1.2 Important properties

- **Greedy-choice property:** There is an optimal solution that begins with the greedy choice (or can be transformed to one without worsening it).
- **Optimal substructure:** After making a valid choice, the remaining problem can be solved optimally to complete an optimal solution.

Optimal substructure alone does not prove that a greedy choice is valid.

### 7.1.3 Activity Selection Problem

**Problem:** Select the maximum number of mutually compatible activities, each with a start time and finish time, using one resource.

**Greedy rule:** Choose the activity that finishes earliest among the activities compatible with those already selected.

### Algorithm

1. Sort activities by increasing finish time.
2. Select the first activity.
3. For each next activity, select it if its start time is at least the finish time of the last selected activity (for the usual convention that touching endpoints is allowed).

```text
ACTIVITY-SELECTION(activities)
    sort activities by increasing finish time
    select the first activity
    lastFinish = finish time of first activity

    for each remaining activity in sorted order
        if activity.start >= lastFinish
            select activity
            lastFinish = activity.finish
```

### Example

Activities:

| Activity | Start | Finish |
|---|---:|---:|
| A1 | 1 | 3 |
| A2 | 2 | 5 |
| A3 | 4 | 6 |
| A4 | 6 | 7 |
| A5 | 5 | 8 |
| A6 | 8 | 9 |

By earliest finish time, choose A1 (1–3), A3 (4–6), A4 (6–7), A6 (8–9).

The selected set contains four compatible activities.

### Complexity

Sorting: `O(n log n)`; scan: `O(n)`. Overall: `O(n log n)`. If activities are already sorted by finish time, the scan takes `O(n)`.

### Why not choose the shortest activity?

The shortest activity may be in the middle and prevent selecting two or more compatible activities around it. The earliest-finish rule is the one justified for this problem.

### 7.1.4 Fractional Knapsack

**Problem:** Each item has value `vᵢ` and weight `wᵢ`. A bag has capacity `W`. Fractions of items are allowed. Maximize total value without exceeding capacity.

**Greedy rule:** Sort items by decreasing value-to-weight ratio:

\[
r_i=\frac{v_i}{w_i}
\]

Take as much as possible of the item with the highest ratio, then continue.

### Example

Capacity `W=50`:

| Item | Value | Weight | Value/weight |
|---|---:|---:|---:|
| A | 60 | 10 | 6 |
| B | 100 | 20 | 5 |
| C | 120 | 30 | 4 |

Take all of A (weight 10, value 60), all of B (weight 20, value 100), and 20 units of C (two-thirds of it, value 80).

Total value:

\[
60+100+120\left(\frac{20}{30}\right)=240
\]

### Complexity

Sorting by ratio takes `O(n log n)`; selecting items takes `O(n)`. Total: `O(n log n)`.

**Important:** The greedy ratio method solves fractional knapsack, not the general 0/1 knapsack problem.

### 7.1.5 Job Sequencing with Deadlines

In a common version, each job takes one unit of time, has a deadline and a profit, and earns profit only if completed by its deadline.

A standard greedy approach is:

1. Sort jobs by decreasing profit.
2. For each job, place it in the latest still-free time slot at or before its deadline.
3. Skip the job if no such slot exists.

The latest-slot choice leaves earlier slots available for jobs with tighter deadlines. Complexity depends on the implementation: a simple slot search can be `O(nD)` after sorting, where `D` is the maximum deadline; disjoint-set optimization can improve slot allocation.

This method relies on the unit-time job model and the stated profit/deadline assumptions.

### 7.1.6 Huffman Coding

Huffman coding creates a prefix-free variable-length code that minimizes the weighted external path length for given symbol frequencies.

Greedy rule:

1. Put all symbols into a min-priority queue by frequency.
2. Remove the two least-frequent nodes.
3. Combine them into a new node whose frequency is their sum.
4. Insert the combined node back.
5. Repeat until one tree remains.

With a binary heap, time is `O(n log n)`. Prefix-free means no codeword is the prefix of another, allowing unambiguous decoding.

### 7.1.7 When greedy is not enough

**0/1 knapsack counterexample:** Capacity 50; items `(value, weight)` are `(60,10)`, `(100,20)`, `(120,30)`. Ratio-greedy chooses the first two items (weight 30, value 160), then cannot take the third. The optimal 0/1 choice is the second and third items (weight 50, value 220). Thus ratio-greedy is not correct for general 0/1 knapsack.

### 7.1.8 How to prove a greedy algorithm

Common proof methods:

- **Exchange argument:** Start with an optimal solution. Show that replacing one of its choices with the greedy choice does not make it worse. Continue until it agrees with the greedy solution.
- **Staying-ahead argument:** Show that after every step the greedy partial solution is at least as good as a competing solution according to a useful measure.
- **Cut property:** For MSTs, a lightest edge crossing a cut is safe (with appropriate treatment of ties).

A worked greedy rule without a correctness argument may solve examples but does not establish that the method always works.

## 7.2 Dynamic Programming

### 7.2.1 Basic idea

Dynamic programming (DP) solves a problem by breaking it into smaller subproblems, solving each subproblem once, and storing its answer for reuse.

DP is especially useful when a problem has:

1. **Overlapping subproblems:** The same smaller problem is solved repeatedly by a straightforward recursive method.
2. **Optimal substructure:** An optimal solution can be constructed from optimal solutions to smaller subproblems.

### 7.2.2 Two main approaches

| Approach | Meaning |
|---|---|
| Memoization (top-down) | Use recursion; store a result when a state is first solved; reuse it later. |
| Tabulation (bottom-up) | Fill a table iteratively, starting from base cases and following a valid dependency order. |

Both can have the same asymptotic time and space complexity. Memoization may compute only reachable states; tabulation may have simpler iteration and lower function-call overhead.

### 7.2.3 Fibonacci example

Definition:

\[
F(0)=0,\quad F(1)=1
\]

\[
F(n)=F(n-1)+F(n-2),\quad n\geq2
\]

Naive recursion recomputes many values. Its time is exponential (`Θ(φⁿ)` up to a constant factor, and commonly bounded by `O(2ⁿ)`).

**Bottom-up DP:**

```text
FIB(n)
    if n <= 1
        return n
    dp[0] = 0
    dp[1] = 1
    for i = 2 to n
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

Time: `O(n)`. Table space: `O(n)`. Because each step needs only the previous two values, the space can be reduced to `O(1)`.

### 7.2.4 0/1 Knapsack using DP

There are `n` items. Item `i` has weight `wᵢ` and value `vᵢ`. Capacity is `W`. Each item can be selected at most once.

Define:

\[
DP[i][c]=\text{maximum value using the first }i\text{ items with capacity }c
\]

Base cases:

\[
DP[0][c]=0,\quad DP[i][0]=0
\]

Recurrence:

If `wᵢ > c`, item `i` cannot be selected:

\[
DP[i][c]=DP[i-1][c]
\]

Otherwise choose the better of excluding and including item `i`:

\[
DP[i][c]=\max\left(DP[i-1][c],\ v_i+DP[i-1][c-w_i]\right)
\]

### Complexity

There are `(n+1)(W+1)` states and constant work per state:

- Time: `O(nW)`.
- Space: `O(nW)` for the full table.
- Space can be reduced to `O(W)` using a one-dimensional array, iterating capacities **downward** from `W` to `wᵢ` for each item.

`O(nW)` is pseudo-polynomial, not polynomial in the number of input bits in general, because the numeric value `W` may be exponentially large relative to its bit-length.

### 7.2.5 Why iterate capacity downward in 0/1 knapsack?

In a one-dimensional implementation, downward iteration ensures that `dp[c-wᵢ]` still refers to the previous item layer. If capacities are iterated upward, the current item may be reused several times, changing the problem into the unbounded-knapsack variant.

### 7.2.6 Longest Common Subsequence (LCS)

A **subsequence** preserves relative order but need not use consecutive characters.

For strings `X` of length `m` and `Y` of length `n`, define `L[i][j]` as the LCS length of the first `i` characters of `X` and first `j` characters of `Y`.

Base cases:

\[
L[i][0]=0,\quad L[0][j]=0
\]

Recurrence:

If `X[i-1] == Y[j-1]`:

\[
L[i][j]=1+L[i-1][j-1]
\]

Otherwise:

\[
L[i][j]=\max(L[i-1][j],L[i][j-1])
\]

Time: `O(mn)`. Full-table space: `O(mn)`. Length-only computation can use `O(min(m,n))` space with carefully arranged rolling rows. Reconstructing an actual subsequence generally needs additional information or a retained table.

### Solved LCS example

`X = ABCDGH`, `Y = AEDFHR`.

One LCS is `ADH`, with length 3.

The DP table is filled using the match/mismatch recurrence. The answer is the bottom-right cell, `L[6][6] = 3`.

### 7.2.7 Matrix Chain Multiplication

Given matrices `A₁, A₂, ..., Aₙ`, matrix multiplication is associative, so the final product is the same for every parenthesization, but the number of scalar multiplications can differ.

Let matrix `Aᵢ` have dimensions `p[i-1] × p[i]`. Define:

\[
M[i][j]=\text{minimum scalar multiplications to compute }A_i\cdots A_j
\]

Base case:

\[
M[i][i]=0
\]

Recurrence:

\[
M[i][j]=\min_{i\leq k<j}\left(M[i][k]+M[k+1][j]+p[i-1]p[k]p[j]\right)
\]

The last term is the cost of multiplying the two resulting matrices.

Time: `O(n³)`. Space: `O(n²)`.

### 7.2.8 DP problem-solving checklist

1. Define exactly what each DP state means.
2. Identify the choices available from a state.
3. Write the recurrence from those choices.
4. Set correct base cases.
5. Choose a computation order that solves dependencies first.
6. Determine how to obtain the required answer from the table.
7. Count the number of states and work per state.
8. Analyze table and reconstruction space.

A recurrence alone is not a complete DP algorithm; the state meaning, base cases and evaluation order matter.

## 7.3 Divide-and-Conquer

### 7.3.1 Basic idea

Divide-and-conquer solves a problem using three steps:

1. **Divide:** Split the problem into smaller subproblems.
2. **Conquer:** Solve the subproblems, usually recursively.
3. **Combine:** Combine their results into the answer.

Examples: binary search, merge sort and many quick-sort implementations.

### 7.3.2 Recurrence relation

A common recurrence is:

\[
T(n)=aT(n/b)+f(n)
\]

where:

- `a` = number of recursive subproblems,
- `n/b` = approximate size of each subproblem,
- `f(n)` = work done outside the recursive calls (division and combination).

### 7.3.3 Master theorem

For:

\[
T(n)=aT(n/b)+f(n),\quad a\geq1,\ b>1
\]

compare `f(n)` with:

\[
n^{\log_b a}
\]

Let `c = log_b(a)`.

**Case 1:** If `f(n)=O(n^{c-ε})` for some `ε > 0`, then:

\[
T(n)=\Theta(n^c)
\]

**Case 2:** If `f(n)=\Theta(n^c\log^k n)` for `k\geq0`, then:

\[
T(n)=\Theta(n^c\log^{k+1}n)
\]

**Case 3:** If `f(n)=\Omega(n^{c+ε})` for some `ε > 0`, and the regularity condition `a f(n/b) \leq q f(n)` holds for some constant `q < 1` and sufficiently large `n`, then:

\[
T(n)=\Theta(f(n))
\]

Do not apply the Master theorem blindly. It does not directly solve every recurrence, particularly recurrences with unequal subproblem sizes, irregular terms or forms outside its conditions.

### 7.3.4 Solved recurrence examples

**Example 1:**

\[
T(n)=2T(n/2)+n
\]

Here `a=2`, `b=2`, so `n^(log₂2)=n`; `f(n)=n`. Case 2 gives:

\[
T(n)=\Theta(n\log n)
\]

**Example 2:**

\[
T(n)=T(n/2)+1
\]

Here `a=1`, `b=2`, so `n^(log₂1)=1`; `f(n)=1`. Case 2 gives `Θ(log n)`.

**Example 3:**

\[
T(n)=2T(n/2)+n^2
\]

Here `n^(log₂2)=n`; `f(n)=n²`, which is polynomially larger. The regularity condition holds, so Case 3 gives `Θ(n²)`.

### 7.3.5 Divide-and-conquer versus dynamic programming

| Feature | Divide-and-conquer | Dynamic programming |
|---|---|---|
| Subproblems | Commonly independent | Commonly overlap |
| Reuse of results | Often no storage/reuse needed | Stores and reuses results |
| Typical implementation | Recursion | Memoization or tabulation |
| Examples | Merge sort, binary search | LCS, 0/1 knapsack |

A problem may use ideas from more than one technique. The important question is whether subproblem results overlap and whether they are reused.

---

# 8. Graph Fundamentals and Traversals

## 8.1 Graph basics

A graph is commonly represented as:

\[
G=(V,E)
\]

where `V` is the set of vertices (nodes) and `E` is the set of edges (connections).

### Common graph types

| Type | Meaning |
|---|---|
| Undirected | Edges have no direction. |
| Directed (digraph) | Edges have a direction. |
| Weighted | Edges have weights/costs. |
| Unweighted | Edges are treated equally, often with weight 1. |
| Connected (undirected) | A path exists between every pair of vertices. |
| Cyclic | Contains a cycle. |
| Acyclic | Contains no cycle. |
| DAG | Directed acyclic graph. |

For a simple undirected graph with `V` vertices, the maximum number of edges is `V(V-1)/2`. For a simple directed graph without self-loops, it is `V(V-1)`.

## 8.2 Degree

In an undirected graph, the degree of a vertex is the number of incident edges (a self-loop contributes two under the standard convention).

In a directed graph:

- In-degree: number of incoming edges.
- Out-degree: number of outgoing edges.

For an undirected graph:

\[
\sum_{v\in V}\deg(v)=2E
\]

For a directed graph, the sum of all in-degrees and the sum of all out-degrees are each `E`.

## 8.3 Graph representations

### Adjacency matrix

A `V × V` matrix. For an unweighted graph, `A[u][v]` indicates whether an edge exists. For a weighted graph it can store weights, with a suitable representation for no edge.

- Space: `O(V²)`.
- Check whether a particular edge exists: `O(1)`.
- List all neighbours of one vertex: `O(V)` by scanning a row.
- Suitable for dense graphs or frequent edge-existence tests.

### Adjacency list

Each vertex stores a list of its neighbours.

- Space: `O(V+E)`.
- Check a particular edge: up to `O(deg(u))` for vertex `u` in a simple list implementation.
- Iterate over neighbours of `u`: `O(deg(u))`.
- Suitable for sparse graphs and traversal algorithms.

For an undirected graph, each edge is usually stored twice in adjacency lists, once for each endpoint.

## 8.4 Breadth-First Search (BFS)

### Idea

BFS explores a graph level by level. It first visits the start vertex, then all vertices one edge away, then all vertices two edges away, and so on.

It uses a **queue** (FIFO).

### Pseudocode

```text
BFS(G, source)
    mark every vertex unvisited
    create an empty queue Q
    mark source visited
    distance[source] = 0
    enqueue(Q, source)

    while Q is not empty
        u = dequeue(Q)
        for each neighbour v of u
            if v is unvisited
                mark v visited
                distance[v] = distance[u] + 1
                parent[v] = u
                enqueue(Q, v)
```

Mark a vertex visited when it is enqueued, not only when it is dequeued. This prevents it from being inserted into the queue multiple times in the standard implementation.

### Example

Edges: `A-B`, `A-C`, `B-D`, `B-E`, `C-F`. Start at A. If neighbours are considered in alphabetical order, BFS order is:

`A, B, C, D, E, F`.

Distances from A are: A=0; B,C=1; D,E,F=2.

The exact traversal order can depend on the order in which neighbours are stored or examined. Distances do not depend on that neighbour order.

### Complexity

With adjacency lists:

\[
O(V+E)\text{ time},\quad O(V)\text{ auxiliary space}
\]

With an adjacency matrix, scanning the row of each visited vertex can take `O(V²)` time.

### Important property

BFS finds shortest paths measured by the **number of edges** from the source in an unweighted graph (or when all edges have equal weight). It is not a general weighted shortest-path algorithm.

## 8.5 Depth-First Search (DFS)

### Idea

DFS explores as far as possible along one path before backtracking. It can be implemented recursively or using an explicit stack.

### Recursive pseudocode

```text
DFS(G, u)
    mark u visited
    process u
    for each neighbour v of u
        if v is unvisited
            parent[v] = u
            DFS(G, v)
```

To visit every connected component of a graph, run DFS from each vertex that remains unvisited:

```text
for each vertex u
    if u is unvisited
        DFS(G, u)
```

### Complexity

With adjacency lists:

\[
O(V+E)\text{ time},\quad O(V)\text{ auxiliary space}
\]

The `O(V)` space includes visited/parent data and up to `O(V)` recursion depth in the worst case. An explicit stack also may contain `O(V)` vertices.

With an adjacency matrix, time is commonly `O(V²)`.

## 8.6 BFS versus DFS

| Feature | BFS | DFS |
|---|---|---|
| Main data structure | Queue | Stack or recursion |
| Exploration | Level by level | Go deep, then backtrack |
| Shortest path in unweighted graph | Yes | Not guaranteed |
| Finds connected components | Yes | Yes |
| Uses in algorithms | Unweighted shortest paths, level order | Cycle detection, topological sort, component analysis |
| Adjacency-list time | `O(V+E)` | `O(V+E)` |

## 8.7 Connected components

In an undirected graph, a connected component is a maximal set of vertices in which every pair is connected by a path.

Run BFS or DFS from each unvisited vertex. Each new traversal discovers one component. Total time with adjacency lists is `O(V+E)`.

## 8.8 Cycle detection

### Undirected graph using DFS

During DFS, if a visited neighbour is found that is not the current vertex's parent, a cycle exists (for a standard simple undirected graph traversal).

The parent condition is essential: the edge back to the parent is not a cycle by itself.

### Directed graph using DFS colors

Use three states:

- White: not visited.
- Gray: currently on the recursion path (active).
- Black: fully processed.

An edge to a gray vertex is a back edge and indicates a directed cycle. An edge to a black vertex does not by itself prove a cycle.

Another method uses topological sorting: a directed graph is acyclic exactly when a topological ordering exists.

## 8.9 Topological sorting

A topological ordering of a directed graph is a linear order of vertices such that for every edge `u → v`, `u` appears before `v`.

It exists if and only if the directed graph is a DAG.

### DFS method

Run DFS and place each vertex at the front of the ordering when its DFS call finishes. Reversing finishing order produces a topological order if the graph is acyclic. Detect back edges to report a cycle.

### Kahn's algorithm

1. Compute the in-degree of every vertex.
2. Enqueue all vertices with in-degree 0.
3. Remove one from the queue, add it to the order, and decrease the in-degree of each outgoing neighbour.
4. Enqueue a neighbour when its in-degree becomes 0.
5. If fewer than `V` vertices are output, the graph contains a directed cycle.

Time with adjacency lists: `O(V+E)`.

A DAG may have more than one valid topological ordering.

---

# 9. Minimum Spanning Trees

## 9.1 Spanning tree

A **spanning tree** of a connected, undirected graph is a subgraph that:

- Includes every vertex.
- Is connected.
- Contains no cycle.

A spanning tree with `V` vertices has exactly:

\[
V-1\text{ edges}
\]

If a connected graph has more than one spanning tree, their edge sets may differ.

## 9.2 Minimum Spanning Tree (MST)

A **minimum spanning tree** is a spanning tree with the minimum possible sum of edge weights.

\[
W(T)=\sum_{e\in T}w(e)
\]

An MST is defined for a connected, undirected, weighted graph. For a disconnected graph, the corresponding minimum spanning forest is found by taking an MST of each connected component.

### Important properties

- Every spanning tree has exactly `V-1` edges.
- An MST has minimum total edge weight; it does not necessarily provide shortest paths from a particular source.
- Negative edge weights are allowed in MST problems.
- If all edge weights are distinct, the MST is unique.
- If equal weights exist, multiple MSTs may exist.

## 9.3 Cut and cycle properties

### Cut property

A cut divides the vertices into two nonempty groups. An edge crosses the cut if its endpoints lie in different groups.

A minimum-weight edge crossing a cut is safe for some MST (in the presence of ties, it may belong to at least one MST; uniqueness is not guaranteed).

### Cycle property

For a cycle, a uniquely heaviest edge cannot belong to an MST. More generally, a strictly heaviest edge on a cycle can be excluded from every MST.

These properties explain why Prim's and Kruskal's greedy choices are correct.

## 9.4 Kruskal's Algorithm

### Idea

Select edges in increasing order of weight, skipping an edge if it creates a cycle.

### Steps

1. Sort all edges by non-decreasing weight.
2. Initially, each vertex is in its own component.
3. Consider each edge in sorted order.
4. If its endpoints belong to different components, add it to the MST and union the components.
5. Stop after selecting `V-1` edges (for a connected graph).

### Pseudocode

```text
KRUSKAL(G)
    MST = empty set
    make a separate set for every vertex
    sort edges by increasing weight

    for each edge (u, v) in sorted order
        if FIND(u) != FIND(v)
            add (u, v) to MST
            UNION(u, v)
        if MST contains V - 1 edges
            break

    return MST
```

### Disjoint Set Union (DSU)

DSU supports:

- `MAKE-SET(x)`: create a set containing `x`.
- `FIND(x)`: identify the representative of the set containing `x`.
- `UNION(x,y)`: merge the sets containing `x` and `y`.

With path compression and union by rank/size, a sequence of operations takes near-constant amortized time per operation, formally `O(α(V))` amortized, where `α` is the inverse Ackermann function.

### Complexity

Sorting edges: `O(E log E)`. DSU operations over the edges are nearly linear overall. Total:

\[
O(E\log E)
\]

Since `E` is at most `V(V-1)/2` in a simple undirected graph, `log E = O(log V)`; the bound is often written `O(E log V)`.

## 9.5 Prim's Algorithm

### Idea

Grow one tree. Start from any vertex and repeatedly add the minimum-weight edge that connects a vertex already in the tree to a vertex outside it.

### Pseudocode (min-priority queue version)

```text
PRIM(G, start)
    key[v] = infinity for every vertex v
    parent[v] = NIL for every vertex v
    key[start] = 0
    insert all vertices into a min-priority queue

    while priority queue is not empty
        u = EXTRACT-MIN()
        for each edge (u, v, weight) where v is still in queue
            if weight < key[v]
                key[v] = weight
                parent[v] = u
                DECREASE-KEY(v, weight)

    MST edges are (parent[v], v) for vertices with a parent
```

The implementation must handle disconnected graphs if it is expected to produce a minimum spanning forest; a single start vertex only reaches its connected component.

### Complexity by implementation

| Implementation | Time |
|---|---:|
| Adjacency matrix, simple array selection | `O(V²)` |
| Adjacency list + binary heap | `O((V+E) log V)` (often written `O(E log V)` for connected graphs with suitable handling) |
| Fibonacci heap theoretical bound | `O(E + V log V)` |

### Prim versus Kruskal

| Feature | Prim | Kruskal |
|---|---|---|
| Strategy | Grows one tree | Builds a forest and joins components |
| Main selection | Cheapest edge crossing current tree cut | Globally lightest remaining edge that does not form a cycle |
| Common data structure | Priority queue | Sorting + DSU |
| Often convenient for | Dense graphs with matrix implementation; also sparse with a heap | Sparse edge-list graphs |
| Cycle handling | A new vertex is added to the tree | DSU detects whether endpoints are already connected |

## 9.6 Solved MST example

Consider edges:

| Edge | Weight |
|---|---:|
| A-B | 1 |
| A-C | 4 |
| B-C | 2 |
| B-D | 5 |
| C-D | 3 |
| C-E | 6 |
| D-E | 7 |

Using Kruskal, sort the edges:

`AB(1), BC(2), CD(3), AC(4), BD(5), CE(6), DE(7)`.

- Select AB(1).
- Select BC(2).
- Select CD(3).
- Skip AC(4), because A and C are already connected; it would create a cycle.
- Skip BD(5), for the same reason.
- Select CE(6).

There are `V-1 = 4` selected edges. Total MST weight:

\[
1+2+3+6=12
\]

---

# 10. Shortest-Path Algorithms

## 10.1 What is a shortest path?

A path's weight is the sum of the weights of its edges. A shortest path between two vertices has minimum total weight among all paths connecting them.

Different algorithms apply to different edge-weight conditions. Selecting the wrong algorithm can produce incorrect results.

## 10.2 Algorithm selection guide

| Situation | Suitable algorithm |
|---|---|
| Unweighted graph / equal positive edge costs, single source | BFS |
| Weighted DAG, single source (negative edges allowed) | Topological-order relaxation |
| Non-negative edge weights, single source | Dijkstra |
| Negative edge weights, single source; need to detect reachable negative cycle | Bellman-Ford |
| All-pairs shortest paths | Floyd-Warshall |

## 10.3 Relaxation

Many shortest-path algorithms use **relaxation**.

For edge `u → v` with weight `w`:

\[
\text{if }d[u]+w<d[v],\quad d[v]=d[u]+w
\]

Also set `parent[v] = u` when the distance is improved.

Relaxation asks whether reaching `v` through `u` is better than the best route known so far.

## 10.4 BFS for unweighted shortest paths

BFS explores vertices in increasing number of edges from the source. Set:

\[
d[source]=0,\qquad d[v]=d[u]+1
\]

when first discovering an unvisited neighbour `v` of `u`.

Time with adjacency lists: `O(V+E)`. It finds shortest paths in an unweighted graph, but not necessarily minimum-weight paths in a general weighted graph.

## 10.5 Shortest paths in a DAG

A DAG can contain negative edge weights and still have no directed cycles.

Algorithm:

1. Compute a topological ordering.
2. Set source distance to 0 and all other distances to infinity.
3. Process vertices in topological order.
4. Relax every outgoing edge of the current vertex.

Time: `O(V+E)` with adjacency lists. It works with negative weights because a DAG has no cycle that can repeatedly reduce a path cost.

## 10.6 Dijkstra's Algorithm

### Condition

Dijkstra's algorithm requires **non-negative edge weights** for its standard correctness guarantee.

### Idea

It repeatedly finalizes the not-yet-finalized vertex with the smallest tentative distance. It then relaxes that vertex's outgoing edges.

### Pseudocode (priority queue)

```text
DIJKSTRA(G, source)
    dist[v] = infinity for every vertex v
    parent[v] = NIL for every vertex v
    dist[source] = 0
    insert (0, source) into min-priority queue

    while queue is not empty
        (du, u) = EXTRACT-MIN()
        if du != dist[u]
            continue                 // ignore stale entry

        for each edge (u, v, w)
            if dist[u] + w < dist[v]
                dist[v] = dist[u] + w
                parent[v] = u
                insert (dist[v], v) into queue

    return dist, parent
```

Some implementations use a decrease-key operation instead of inserting duplicate entries. Complexity depends on the priority-queue implementation.

### Complexity

- Adjacency matrix + simple vertex selection: `O(V²)`.
- Adjacency list + binary heap: `O((V+E) log V)` for the common implementation.
- A Fibonacci heap gives the theoretical bound `O(E + V log V)`.

### Why negative edges cause a problem

Dijkstra relies on the fact that once the smallest tentative-distance vertex is selected, no later route can improve it. A negative edge can violate this assumption.

### Counterexample

Edges: `S→A` weight 2, `S→B` weight 5, `B→A` weight -10.

Dijkstra may finalize A with distance 2 before considering the route through B, whose total is `5 + (-10) = -5`. The standard algorithm is therefore not correct for arbitrary negative edges.

## 10.7 Bellman-Ford Algorithm

### Condition and use

Bellman-Ford supports negative edge weights and can detect a negative-weight cycle reachable from the source.

### Idea

A shortest simple path (when no reachable negative cycle affects it) uses at most `V-1` edges. Repeatedly relax every edge `V-1` times.

### Pseudocode

```text
BELLMAN-FORD(G, source)
    dist[v] = infinity for every vertex v
    dist[source] = 0

    repeat V - 1 times
        for each edge (u, v, w)
            if dist[u] != infinity and dist[u] + w < dist[v]
                dist[v] = dist[u] + w
                parent[v] = u

    for each edge (u, v, w)
        if dist[u] != infinity and dist[u] + w < dist[v]
            report reachable negative-weight cycle

    return dist, parent
```

The `dist[u] != infinity` check prevents treating an unreachable vertex as a valid starting point for relaxation.

### Complexity

- Time: `O(VE)`.
- Space: `O(V)` for distances and parents, excluding graph storage.

A negative cycle that is not reachable from the source does not affect source-reachable shortest paths and is not detected by the source-based check above.

## 10.8 Floyd-Warshall Algorithm

### Purpose

Floyd-Warshall finds shortest-path distances between **all pairs** of vertices.

It supports negative edge weights but assumes there is no negative-weight cycle if finite shortest-path distances are required.

### Idea

At stage `k`, determine whether going from `i` to `j` through vertex `k` is shorter than the best route known so far.

### Recurrence

\[
D^{(k)}[i][j]=\min\left(D^{(k-1)}[i][j],\ D^{(k-1)}[i][k]+D^{(k-1)}[k][j]\right)
\]

In-place form:

\[
d[i][j]=\min(d[i][j],d[i][k]+d[k][j])
\]

### Pseudocode

```text
FLOYD-WARSHALL(dist)
    for k = 0 to V - 1
        for i = 0 to V - 1
            for j = 0 to V - 1
                if dist[i][k] != infinity and dist[k][j] != infinity
                    dist[i][j] = min(dist[i][j],
                                     dist[i][k] + dist[k][j])
```

Initialize:

- `dist[i][i] = 0`.
- `dist[u][v]` to the minimum direct edge weight from `u` to `v`, if one exists.
- Infinity if no direct path exists.

### Complexity

- Time: `O(V³)`.
- Space: `O(V²)` for the distance matrix.

After the algorithm, if `dist[v][v] < 0` for any vertex `v`, a negative-weight cycle exists.

The order of the three loops is important: the intermediate-vertex loop `k` must be the outer loop in the standard in-place recurrence.

## 10.9 Dijkstra versus Bellman-Ford versus Floyd-Warshall

| Feature | Dijkstra | Bellman-Ford | Floyd-Warshall |
|---|---|---|---|
| Main purpose | Single-source | Single-source | All-pairs |
| Negative edges | Not supported by standard guarantee | Supported | Supported |
| Detect negative cycle? | No | Yes, reachable from source | Yes, by negative diagonal after completion |
| Typical time | `O((V+E) log V)` with binary heap | `O(VE)` | `O(V³)` |
| Typical distance storage | `O(V)` | `O(V)` | `O(V²)` |

## 10.10 Solved shortest-path example

Directed edges:

- `S→A = 4`
- `S→B = 1`
- `B→A = 2`
- `A→C = 1`
- `B→C = 5`

All weights are non-negative, so Dijkstra is suitable.

Start: `dist[S]=0`; all other distances are infinity.

1. Select S: update A=4 and B=1.
2. Select B (smallest tentative distance 1): update A to `1+2=3`; update C to `1+5=6`.
3. Select A (distance 3): update C to `3+1=4`.
4. Select C (distance 4): no improvement.

Final distances:

| Vertex | Shortest distance from S | One shortest path |
|---|---:|---|
| S | 0 | S |
| B | 1 | S → B |
| A | 3 | S → B → A |
| C | 4 | S → B → A → C |

---

# 11. Important Complexity Summary

## 11.1 Searching and sorting

| Algorithm | Worst-case time | Auxiliary space (typical) |
|---|---:|---:|
| Linear search | `O(n)` | `O(1)` |
| Iterative binary search | `O(log n)` | `O(1)` |
| Bubble sort | `O(n²)` | `O(1)` |
| Selection sort | `O(n²)` | `O(1)` |
| Insertion sort | `O(n²)` | `O(1)` |
| Merge sort | `O(n log n)` | `O(n)` |
| Quick sort | `O(n²)` | `O(n)` worst recursion stack |
| Heap sort | `O(n log n)` | `O(1)` iterative |
| Counting sort | `O(n+k)` | `O(n+k)` |
| Radix sort | `O(d(n+k))` | commonly `O(n+k)` |

## 11.2 Graph algorithms

| Algorithm | Purpose | Time (common implementation) |
|---|---|---:|
| BFS | Traversal / unweighted single-source shortest paths | `O(V+E)` with adjacency list |
| DFS | Traversal / components / cycle-related tasks | `O(V+E)` with adjacency list |
| Topological sort | Order vertices of a DAG | `O(V+E)` |
| Kruskal | Minimum spanning tree | `O(E log E)` |
| Prim (matrix) | Minimum spanning tree | `O(V²)` |
| Prim (binary heap + adjacency list) | Minimum spanning tree | `O((V+E) log V)` |
| DAG shortest path | Single-source shortest paths in DAG | `O(V+E)` |
| Dijkstra (binary heap) | Single-source, non-negative edges | `O((V+E) log V)` |
| Bellman-Ford | Single-source, negative edges allowed | `O(VE)` |
| Floyd-Warshall | All-pairs shortest paths | `O(V³)` |

## 11.3 Design techniques

| Technique | Main idea | Examples |
|---|---|---|
| Greedy | Make a justified locally optimal choice | Activity selection, fractional knapsack, MST |
| Dynamic programming | Store answers to overlapping subproblems | 0/1 knapsack, LCS, matrix-chain multiplication |
| Divide-and-conquer | Divide, solve recursively, combine | Binary search, merge sort, quick sort |

---

# 12. Common GATE Traps

1. **Big-O and worst case are not synonyms.** Worst case describes the input case; Big-O describes an asymptotic upper bound.
2. **Binary search needs sorted data** and a suitable way to access the middle element efficiently.
3. **Binary search on a linked list** does not generally achieve `O(log n)` time because reaching the middle is not `O(1)`.
4. **Selection sort remains `Θ(n²)` even on sorted input** because it still searches for the minimum in each unsorted suffix.
5. **Insertion sort is `Θ(n)` on already sorted input** under the usual implementation.
6. **Merge sort is `Θ(n log n)` in all cases** for the usual implementation, but array merge needs `O(n)` auxiliary storage.
7. **Quick sort has `O(n²)` worst-case time**, even though its expected time with randomized pivoting is `O(n log n)`.
8. **Build-heap is `O(n)`, not `O(n log n)`.**
9. **Counting sort is not a general comparison sort.** Its efficiency depends on a manageable key range.
10. **Hash-table `O(1)` is expected/common under assumptions, not a universal worst-case guarantee.**
11. **Linear probing causes primary clustering.**
12. **Greedy fractional knapsack does not solve general 0/1 knapsack.**
13. **Optimal substructure alone does not prove a greedy strategy.**
14. **DP time is number of states × work per state.** Do not count only the recurrence depth.
15. **0/1 knapsack one-dimensional DP must iterate capacity downward.**
16. **BFS uses a queue; DFS uses a stack or recursion.**
17. **BFS gives shortest paths by edge count in an unweighted graph**, not by arbitrary edge weights.
18. **An adjacency-list traversal is `O(V+E)`, not simply `O(E)`**, because all vertices may need to be initialized or visited, including isolated vertices.
19. **A spanning tree has `V-1` edges.** A selected set with fewer edges cannot connect all vertices; a connected acyclic graph cannot have extra edges.
20. **MST and shortest-path tree are different.** An MST minimizes total tree-edge weight; a shortest-path tree preserves distances from one source.
21. **Negative edge weights are allowed in MST algorithms.**
22. **Dijkstra requires non-negative edge weights** for its standard guarantee.
23. **Bellman-Ford detects negative cycles reachable from the source** in its source-based form.
24. **Floyd-Warshall is all-pairs and takes `O(V³)` time and `O(V²)` space.**
25. **A DAG can have negative edge weights**, and topological relaxation still works.
26. **A topological order exists only for a DAG.** There may be multiple valid orders.

---

# 13. Quick Revision Notes

## 13.1 Complexity reminders

- Consecutive blocks: add costs and keep the dominant term.
- Nested loops: multiply iteration counts only when their bounds are independent; otherwise sum carefully.
- Repeated halving/doubling: usually `O(log n)`.
- One recursive call on `n-1`: often linear depth.
- One recursive call on `n/2`: often logarithmic depth.
- Time and stack space are separate analyses.
- For DP: `number of states × transition work per state`.

## 13.2 Searching and sorting

- Linear search: sorted or unsorted, worst `O(n)`.
- Binary search: sorted random-access data, worst `O(log n)`.
- Insertion sort: stable, in-place, adaptive; best `O(n)`, worst `O(n²)`.
- Selection sort: `O(n²)` in all cases; few swaps; generally unstable.
- Bubble sort with early stop: best `O(n)`, worst `O(n²)`.
- Merge sort: stable, `O(n log n)`, array auxiliary space `O(n)`.
- Quick sort: expected `O(n log n)`, worst `O(n²)`; usually not stable.
- Heap sort: `O(n log n)` worst-case; build heap `O(n)`; in-place and unstable.
- Comparison sort worst-case lower bound: `Ω(n log n)` comparisons.

## 13.3 Hashing

- Collision: different keys get the same table index.
- Load factor: `α = n/m`.
- Chaining: expected `O(1+α)` under uniform hashing; worst `O(n)`.
- Linear probing: `h(k)+i mod m`; primary clustering.
- Quadratic probing: quadratic offsets; can have secondary clustering.
- Double hashing: second hash determines step; choose parameters that cover the table.
- Open-addressing deletion often needs a tombstone.

## 13.4 Design methods

- Greedy: local choice with proof; activity selection, fractional knapsack and MST.
- DP: overlapping subproblems + optimal substructure; memoization or tabulation.
- 0/1 knapsack: `O(nW)` time; downward capacity loop in 1D DP.
- LCS: `O(mn)` time.
- Matrix-chain multiplication: `O(n³)` time and `O(n²)` space.
- Divide-and-conquer: divide, conquer, combine.
- Master theorem compares `f(n)` with `n^(log_b a)`.

## 13.5 Graphs

- Adjacency matrix: `O(V²)` space; edge lookup `O(1)`.
- Adjacency list: `O(V+E)` space.
- BFS: queue; `O(V+E)`; unweighted shortest paths.
- DFS: stack/recursion; `O(V+E)`.
- Topological order exists iff the directed graph is acyclic.
- MST: connected, undirected, weighted graph; exactly `V-1` edges.
- Kruskal: sort edges + DSU.
- Prim: grow one tree using minimum crossing edge.
- Dijkstra: non-negative weights.
- Bellman-Ford: negative edges; reachable negative-cycle detection.
- Floyd-Warshall: all pairs; `O(V³)`.

---

# 14. Practice Questions

Try the questions before opening the answer key. Unless stated otherwise, assume standard implementations and express complexity asymptotically.

## A. Conceptual Questions

**Q1.** What is the difference between Big-O, Big-Omega and Big-Theta notation?

**Q2.** Why does binary search require sorted data? What is its worst-case time complexity?

**Q3.** Explain the difference between stable and unstable sorting with a small example.

**Q4.** Why does a hash table still have `O(n)` worst-case search time even though its expected search time may be `O(1)`?

**Q5.** Explain why greedy ratio selection is valid for fractional knapsack but not for all 0/1 knapsack inputs.

**Q6.** What are overlapping subproblems and optimal substructure?

**Q7.** Differentiate BFS and DFS. Which one finds shortest paths in an unweighted graph?

**Q8.** State the difference between a minimum spanning tree and a shortest-path tree.

**Q9.** Why can Dijkstra's algorithm fail when negative edge weights are present?

**Q10.** What does a negative diagonal entry after Floyd-Warshall indicate?

## B. Complexity / NAT Questions

**Q11.** Find the time complexity:

```c
for (int i = 1; i <= n; i *= 2)
    for (int j = 0; j < n; j++)
        count++;
```

**Q12.** Find the number of times the inner statement executes and its asymptotic complexity:

```c
for (int i = 1; i <= n; i++)
    for (int j = 1; j <= i; j++)
        count++;
```

**Q13.** Solve the recurrence `T(n) = 2T(n/2) + n` using the Master theorem.

**Q14.** Solve the recurrence `T(n) = T(n/2) + 1`.

**Q15.** A graph has `V=100` vertices and `E=250` edges. What is the asymptotic traversal time using adjacency lists?

## C. MCQs

**Q16.** Which algorithm has `Θ(n)` best-case time in its standard optimized implementation?

A. Selection sort  
B. Insertion sort  
C. Merge sort  
D. Heap sort

**Q17.** Which sorting algorithm has `O(n²)` worst-case time but `O(n log n)` expected time with randomized pivot selection?

A. Merge sort  
B. Heap sort  
C. Quick sort  
D. Counting sort

**Q18.** Which collision-resolution method is associated with primary clustering?

A. Separate chaining  
B. Linear probing  
C. Double hashing  
D. Rehashing only

**Q19.** Which problem is a standard greedy application?

A. General 0/1 knapsack using value/weight ratio  
B. Activity selection  
C. LCS  
D. Matrix-chain multiplication

**Q20.** Which algorithm is suitable for single-source shortest paths with negative edges, provided negative cycles are handled?

A. Dijkstra  
B. BFS  
C. Bellman-Ford  
D. Prim

## D. MSQ Questions

**Q21.** Select all correct statements.

A. Merge sort has `O(n log n)` worst-case time.  
B. Standard selection sort is stable.  
C. Heap construction using bottom-up heapify takes `O(n)` time.  
D. Binary search can be applied efficiently to a sorted array.

**Q22.** Select all correct statements about graph algorithms.

A. BFS uses a queue.  
B. DFS can be implemented using recursion.  
C. Dijkstra's standard algorithm supports arbitrary negative edge weights.  
D. Topological sorting applies to DAGs.

**Q23.** Select all correct statements about MSTs.

A. An MST of a connected graph with `V` vertices has `V-1` edges.  
B. MST algorithms require all edge weights to be positive.  
C. Kruskal's algorithm commonly uses DSU.  
D. An MST always gives shortest paths from a chosen source.

## E. Application-Based Questions

**Q24.** A sorted array contains duplicates. Describe how to find the first occurrence of a key in `O(log n)` time.

**Q25.** A hash table of size 7 uses `h(k)=k mod 7` and linear probing. Insert keys 10, 17, 24 and 31. Give the final indices.

**Q26.** For fractional knapsack with capacity 40, consider items `(value, weight)` A=`(80,10)`, B=`(100,20)`, C=`(120,30)`. Find the maximum value.

**Q27.** For activities `(start, finish)` A=`(1,4)`, B=`(3,5)`, C=`(0,6)`, D=`(5,7)`, E=`(8,9)`, apply the earliest-finish-time greedy rule. Which activities are selected?

**Q28.** A connected, undirected weighted graph has 6 vertices. How many edges must an MST contain? Does the answer change if some weights are negative?

**Q29.** Choose a suitable algorithm for each case: (a) unweighted single-source shortest paths, (b) non-negative weighted single-source shortest paths, (c) all-pairs shortest paths, (d) a weighted DAG with possible negative edges.

**Q30.** Consider the directed graph with edges `S→A(4)`, `S→B(1)`, `B→A(2)`, `A→C(1)`, `B→C(5)`. Find shortest distances from S.

---

# 15. Detailed Answer Key

## A. Conceptual Answers

**A1.** Big-O is an asymptotic upper bound, Big-Omega is a lower bound, and Big-Theta is a tight bound (both upper and lower). The notation itself does not specify whether the analyzed case is best, average or worst.

**A2.** Binary search decides which half can contain the key based on the ordering of values. Without sorted order, that decision is not justified. Its worst-case time is `Θ(log n)` on a sorted random-access array.

**A3.** A stable sort preserves the original order of equal-key records. For example, `(P,4),(Q,2),(R,4)` becomes `(Q,2),(P,4),(R,4)` in a stable ascending sort. An unstable sort may place R before P even though both have key 4.

**A4.** If many or all keys map to the same index, a chain may contain `n` elements, or an open-addressed search may examine many slots. Therefore worst-case search is `O(n)`. Expected `O(1)` depends on distribution and load-factor assumptions.

**A5.** Fractional knapsack allows taking part of an item, so taking the highest value-per-weight ratio first can be justified by an exchange argument. In 0/1 knapsack each item must be taken completely or not at all; a high-ratio choice can block a better combination of whole items.

**A6.** Overlapping subproblems means the same smaller states occur repeatedly. Optimal substructure means an optimal solution can be constructed from optimal solutions to appropriate smaller subproblems. DP stores these repeated results.

**A7.** BFS uses a queue and explores by distance levels. DFS uses a stack/recursion and explores deeply before backtracking. BFS finds shortest paths by number of edges in an unweighted graph.

**A8.** An MST minimizes the sum of the weights of all selected tree edges. A shortest-path tree preserves shortest distances from one selected source. They optimize different objectives and need not be the same tree.

**A9.** Dijkstra finalizes a vertex when it has the smallest tentative distance, relying on non-negative remaining edges. A later negative edge can create a cheaper path to a vertex already finalized, breaking the reasoning.

**A10.** A negative value `dist[v][v] < 0` indicates a negative-weight cycle reachable from that vertex (and hence present in the graph represented by the matrix).

## B. Complexity / NAT Answers

**A11.** The outer loop doubles `i`, so it runs `Θ(log n)` times. The inner loop runs `n` times per outer iteration. Total:

\[
\boxed{\Theta(n\log n)}
\]

**A12.** The inner statement executes:

\[
1+2+\cdots+n=\frac{n(n+1)}{2}
\]

Therefore the exact count is `n(n+1)/2`, and the asymptotic complexity is:

\[
\boxed{\Theta(n^2)}
\]

**A13.** `a=2`, `b=2`, and `f(n)=n`. Since `n^(log₂2)=n`, this is Master theorem Case 2:

\[
\boxed{T(n)=\Theta(n\log n)}
\]

**A14.** Here `a=1`, `b=2`, and `f(n)=1`. The recursion depth is logarithmic:

\[
\boxed{T(n)=\Theta(\log n)}
\]

**A15.** Adjacency-list traversal is `O(V+E)`. Here it is proportional to `100+250=350` operations up to constant factors. The asymptotic form is `O(V+E)` (and for these fixed numeric values, the count is finite).

## C. MCQ Answers

**A16. B — Insertion sort.** On already sorted input, its inner shifting loop does not shift elements, giving `Θ(n)` time.

**A17. C — Quick sort.** Bad partitions give `O(n²)` worst-case time; randomized pivoting gives `O(n log n)` expected time.

**A18. B — Linear probing.** Consecutive occupied slots can form primary clusters.

**A19. B — Activity selection.** The earliest-finish-time rule produces an optimal selection for the standard activity-selection problem.

**A20. C — Bellman-Ford.** It supports negative edges and can detect a reachable negative-weight cycle.

## D. MSQ Answers

**A21. Correct: A, C and D.** Merge sort has `O(n log n)` worst-case time; bottom-up heap construction is `O(n)`; binary search is efficient on a sorted array. Standard selection sort is not stable.

**A22. Correct: A, B and D.** BFS uses a queue, DFS can be recursive, and topological sorting is for DAGs. Standard Dijkstra does not support arbitrary negative edges.

**A23. Correct: A and C.** A spanning tree has `V-1` edges and Kruskal commonly uses DSU. MST weights can be negative, and an MST does not necessarily give source shortest paths.

## E. Application-Based Solutions

**A24. First occurrence in `O(log n)`:**

Use modified binary search. Initialize `answer = NOT_FOUND`. When `A[mid] == key`, save `mid` and continue left by setting `high = mid - 1`. If `A[mid] < key`, move right; otherwise move left. The final saved index is the first occurrence. Each iteration halves the search interval, so time is `O(log n)` and iterative auxiliary space is `O(1)`.

**A25. Linear probing:**

Table indices are 0 through 6.

- 10 maps to 3 → index 3.
- 17 maps to 3; index 3 occupied → index 4.
- 24 maps to 3; indices 3 and 4 occupied → index 5.
- 31 maps to 3; indices 3, 4 and 5 occupied → index 6.

Final placement: `10→3`, `17→4`, `24→5`, `31→6`.

**A26. Fractional knapsack:**

Ratios:

- A: `80/10 = 8`.
- B: `100/20 = 5`.
- C: `120/30 = 4`.

Take all of A (weight 10, value 80), then all of B (weight 20, value 100). Remaining capacity is 10, so take `10/30` of C for value `120×(10/30)=40`.

Total value:

\[
80+100+40=\boxed{220}
\]

**A27. Activity selection:**

Sort by finish time: A(1,4), B(3,5), C(0,6), D(5,7), E(8,9).

- Select A (finishes at 4).
- B starts at 3, so reject it.
- C starts at 0, so reject it.
- D starts at 5, which is at least 4, so select D.
- E starts at 8, which is at least 7, so select E.

Selected activities: `A, D, E`.

**A28.** An MST contains `V-1 = 6-1 = 5` edges. Negative weights do not change this count and are allowed in MST algorithms.

**A29.**

- (a) BFS.
- (b) Dijkstra.
- (c) Floyd-Warshall (one standard all-pairs choice).
- (d) Topological-order relaxation on the DAG.

**A30. Dijkstra calculation:**

All edge weights are non-negative.

1. Start with `d(S)=0`; other distances are infinity.
2. Process S: `d(A)=4`, `d(B)=1`.
3. Process B (distance 1): improve `d(A)=1+2=3`; set `d(C)=1+5=6`.
4. Process A (distance 3): improve `d(C)=3+1=4`.
5. Process C. No more updates.

Final distances: `d(S)=0`, `d(B)=1`, `d(A)=3`, `d(C)=4`.

One shortest path to C is `S → B → A → C`.

---

# Final Preparation Checklist

Before considering this unit complete, make sure you can:

- [ ] Calculate loop and recursive time complexities.
- [ ] Distinguish Big-O, Big-Omega and Big-Theta.
- [ ] Calculate worst-case time and auxiliary space separately.
- [ ] Trace binary search and modified first/last occurrence searches.
- [ ] Perform sorting passes and identify stable/in-place algorithms.
- [ ] Derive merge-sort and quick-sort recurrences.
- [ ] Explain why bottom-up build-heap is linear.
- [ ] Insert/search/delete using collision-resolution methods.
- [ ] Calculate load factor and trace probe sequences.
- [ ] Identify when greedy choice is valid and provide a proof idea.
- [ ] Form DP states and write correct recurrences.
- [ ] Apply the Master theorem when its conditions hold.
- [ ] Trace BFS, DFS and topological sorting.
- [ ] Find an MST using both Kruskal and Prim.
- [ ] Choose a shortest-path algorithm based on edge-weight conditions.
- [ ] Perform relaxation and detect negative cycles where applicable.

**End of GATE CSE Algorithms study material.**
