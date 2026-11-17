# GATE CSE Study Material: Programming in C and Data Structures

> **Syllabus covered:** Programming in C; recursion; arrays; stacks; queues; linked lists; trees; binary search trees; binary heaps; graphs.  
> **Level:** Fundamentals to GATE CSE problem-solving level.  
> **How to use this guide:** Study the concepts in order, trace the pseudocode by hand, and then solve the practice set before reading its answer key.

---

## Contents

1. [Syllabus checklist and foundations](#1-syllabus-checklist-and-foundations)
2. [Programming in C](#2-programming-in-c)
3. [Recursion](#3-recursion)
4. [Arrays](#4-arrays)
5. [Stacks](#5-stacks)
6. [Queues](#6-queues)
7. [Linked lists](#7-linked-lists)
8. [Trees](#8-trees)
9. [Binary search trees](#9-binary-search-trees)
10. [Binary heaps](#10-binary-heaps)
11. [Graphs](#11-graphs)
12. [Comparisons and complexity summary](#12-comparisons-and-complexity-summary)
13. [GATE problem-solving approach and common traps](#13-gate-problem-solving-approach-and-common-traps)
14. [Practice questions](#14-practice-questions)
15. [Detailed answer key](#15-detailed-answer-key)
16. [Quick revision sheet](#16-quick-revision-sheet)

---

# 1. Syllabus checklist and foundations

Use this checklist to track the complete scope of the supplied topic.

- [ ] C program structure, data types, operators, control statements and functions
- [ ] C arrays, strings, pointers, structures and dynamic memory
- [ ] Function calls, parameter passing, memory layout and C pitfalls
- [ ] Recursion: base case, recursive case, tracing, call stack and complexity
- [ ] Recursion examples and recurrence relations
- [ ] Arrays: representation, address calculation and operations
- [ ] Array searching and insertion/deletion costs
- [ ] Stack: operations, implementations and applications
- [ ] Queue: operations, implementations, circular queue, deque and priority queue
- [ ] Linked lists: singly, doubly and circular lists; operations and applications
- [ ] Trees: terminology, properties, representations and traversals
- [ ] Binary search trees: search, insertion, deletion and complexity
- [ ] Binary heaps: min-heap, max-heap, insertion, deletion and heap construction
- [ ] Graphs: terminology, representations, BFS and DFS
- [ ] Complexity analysis, edge cases, practice questions and solutions

## 1.1 What is a data structure?

A **data structure** is a way of arranging and storing data so that operations on that data can be performed efficiently.

For example, suppose an application stores the roll numbers of 1,000 students.

- An array is useful when fast access by position is required.
- A stack is useful when the most recently added item must be processed first.
- A queue is useful when items must be processed in arrival order.
- A linked list is useful when nodes must be inserted or removed by changing links.
- A tree is useful for representing hierarchical data.
- A heap is useful when the smallest or largest item must be obtained quickly.
- A graph is useful for representing connections such as roads or computer networks.

A data structure is usually studied through its **operations**, its **implementation**, and the **time and space** required by those operations.

## 1.2 Abstract data type (ADT)

An **abstract data type** describes what operations are available and what they mean, without fixing how they are implemented.

For example, a Stack ADT supports operations such as:

- `push(x)`: insert `x` at the top.
- `pop()`: remove and return the top element.
- `peek()`: return the top element without removing it.
- `isEmpty()`: check whether the stack contains no elements.

A stack can be implemented using an array or a linked list. Both implementations can provide the same Stack ADT, even though their internal representations are different.

## 1.3 Time and space complexity

**Time complexity** describes how the number of basic operations grows as the input size grows. **Space complexity** describes how the memory requirement grows.

Let `n` be the input size.

| Notation | Meaning | Example |
|---|---|---|
| `O(1)` | Constant growth | Accessing `A[i]` in an array |
| `O(log n)` | Logarithmic growth | Binary search in a sorted array |
| `O(n)` | Linear growth | Traversing an array |
| `O(n log n)` | Linearithmic growth | Heap sort |
| `O(n^2)` | Quadratic growth | Two nested loops, each running `n` times |
| `O(2^n)` | Exponential growth | Naive recursive Fibonacci (upper-bound description) |

### Best, average and worst cases

- **Best case:** the least work for an input of size `n`.
- **Average case:** the expected work under an assumed input distribution.
- **Worst case:** the maximum work for an input of size `n`.

For linear search in an array of `n` elements:

- Best case: the item is first, so `O(1)`.
- Worst case: the item is last or absent, so `O(n)`.
- Under a simple model where each position is equally likely, the average number of comparisons for a successful search is `(n + 1) / 2`, which is `O(n)`.

### Auxiliary space

**Auxiliary space** is the extra memory used by an algorithm, excluding the input storage itself. For example, an iterative array traversal uses `O(1)` auxiliary space; a recursive traversal may use `O(h)` call-stack space, where `h` is the recursion depth.

---

# 2. Programming in C

C is a procedural, general-purpose programming language. In this syllabus, C is important because it helps explain how data is stored, how functions execute, and how data structures are implemented using arrays, pointers and dynamically allocated memory.

## 2.1 Basic structure of a C program

```c
#include <stdio.h>

int main(void) {
    int number = 10;
    printf("Number = %d\n", number);
    return 0;
}
```

Explanation:

1. `#include <stdio.h>` makes standard input/output declarations such as `printf` available.
2. `int main(void)` is the program's entry function in a hosted C program.
3. `int number = 10;` declares and initializes an integer variable.
4. `printf` prints formatted output.
5. `return 0;` indicates successful termination to the environment.

## 2.2 Variables and common data types

A **variable** is a named object whose value may be used or changed during program execution.

| Type | Typical use | Example |
|---|---|---|
| `char` | Character or small integer value | `char grade = 'A';` |
| `int` | Integer values | `int count = 25;` |
| `float` | Single-precision floating-point value | `float rate = 2.5f;` |
| `double` | Double-precision floating-point value | `double pi = 3.14159;` |
| `void` | No value / generic pointer type | `void f(void);` |

The exact sizes of C data types are implementation-dependent, subject to the guarantees of the C standard. Do not assume that `int` is always exactly 4 bytes or that a pointer is always 8 bytes. Use `sizeof(type)` or `sizeof object` when the actual size is needed.

```c
printf("%zu\n", sizeof(int));
```

`sizeof` produces a value of type `size_t`, so `%zu` is the appropriate standard format specifier for printing it.

## 2.3 Operators and expressions

Common operator groups:

| Group | Operators | Purpose |
|---|---|---|
| Arithmetic | `+ - * / %` | Arithmetic operations |
| Relational | `< <= > >= == !=` | Comparisons |
| Logical | `&& || !` | Boolean conditions |
| Assignment | `= += -= *= /=` | Assigning or updating values |
| Increment/decrement | `++ --` | Add or subtract one |
| Address/dereference | `& *` | Obtain an address / access pointed-to object |
| Conditional | `condition ? a : b` | Choose one of two expressions |

### Integer division and remainder

When both operands of `/` are integers, C performs integer division and discards the fractional part, with the result truncated toward zero.

```c
int a = 7 / 2;   // 3
int b = -7 / 2;  // -3
int r = 7 % 2;   // 1
```

For integer operands, the remainder has the sign of the dividend or is zero. Do not treat `%` as a percentage operator.

### Pre-increment and post-increment

- `++i` increments `i` and the expression produces the new value.
- `i++` produces the old value and then increments `i` as part of evaluating the full expression.

```c
int i = 4;
int a = ++i; // i = 5, a = 5

int j = 4;
int b = j++; // b = 4, j = 5
```

Avoid expressions that modify the same scalar object multiple times without the sequencing required by C. Such expressions can have undefined behavior; they are not reliable puzzles to solve by guessing an evaluation order.

### Short-circuit evaluation

For `A && B`, `B` is not evaluated if `A` is false. For `A || B`, `B` is not evaluated if `A` is true.

```c
if (p != NULL && p->value == 10) {
    /* Safe to evaluate p->value after p != NULL is true. */
}
```

This is useful for checking a pointer before dereferencing it.

## 2.4 Decision and looping statements

```c
if (condition) {
    /* statements */
} else {
    /* other statements */
}

for (int i = 0; i < n; i++) {
    /* repeated n times */
}

while (condition) {
    /* repeat while condition is true */
}

do {
    /* executes at least once */
} while (condition);
```

A `break` exits the nearest enclosing loop or `switch`. A `continue` skips the remaining statements in the current loop iteration and proceeds to the next iteration.

## 2.5 Functions and parameter passing

A function groups a task into a reusable unit.

```c
int square(int x) {
    return x * x;
}

int main(void) {
    int result = square(5);
    return 0;
}
```

C uses **pass-by-value**: a function receives the value of each argument. When a pointer is passed, the pointer value (an address) is copied. The function can use that address to modify the object it points to.

```c
void change(int x) {
    x = 100;       // Changes only the local copy.
}

void change_original(int *p) {
    *p = 100;      // Changes the caller's object through the pointer.
}
```

```c
int main(void) {
    int a = 5;
    change(a);
    /* a is still 5 */
    change_original(&a);
    /* a is now 100 */
    return 0;
}
```

## 2.6 Arrays in C

An array stores a fixed number of elements of the same type in contiguous memory.

```c
int marks[5] = {70, 80, 65, 90, 75};
```

Valid indexes are `0` through `4`. C does not automatically check array bounds. Accessing an element outside the array's valid range causes undefined behavior.

In most expressions, an array expression is converted to a pointer to its first element. However, an array is not itself a pointer. For example, `sizeof marks` gives the size of the complete array in the scope where `marks` is an array; inside a function parameter declared as `int marks[]`, the parameter is adjusted to a pointer type.

## 2.7 Pointers

A **pointer** stores the address of an object or function (depending on the pointer type).

```c
int x = 20;
int *p = &x;

printf("%d\n", *p); // 20
*p = 35;             // x becomes 35
```

- `&x` means the address of `x`.
- `p` stores that address.
- `*p` accesses the object at the stored address (dereferencing).

### Pointer arithmetic

If `p` points to an element of an array, `p + 1` points to the next element of that array, not necessarily to the next byte. The address advances by `sizeof(*p)` bytes.

Pointer arithmetic is defined within an array object and one position past its final element. The one-past pointer may be used for comparison or iteration boundaries, but it must not be dereferenced.

### Arrays and pointers are related, but not identical

```c
int a[4] = {10, 20, 30, 40};
int *p = a;

/* a[2], *(a + 2), and p[2] access the third element. */
```

Important distinction:

- `a` in most expressions converts to `&a[0]`.
- `&a` is a pointer to the whole array, with a different pointer type.
- `sizeof(a)` is the size of all four integers when `a` is an actual array in this scope.
- `sizeof(p)` is the size of the pointer itself.

### Two-dimensional arrays

```c
int matrix[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

C stores the elements of a two-dimensional array in **row-major order**: all elements of row 0, followed by row 1, and so on.

A parameter such as `int matrix[][3]` is adjusted to a pointer to an array of 3 integers. It is not equivalent to `int **matrix`.

## 2.8 Strings

A C string is a sequence of `char` values ending with the null character `\0`.

```c
char word[] = "GATE";
/* Stored characters: 'G', 'A', 'T', 'E', '\0' */
```

The array needs space for the terminating null character. For the string literal `"GATE"`, the character array shown above has 5 elements.

Common functions from `<string.h>` include:

- `strlen(s)`: number of characters before `\0` (does not count the terminator).
- `strcmp(a, b)`: lexicographic comparison; returns a negative, zero or positive value.
- `strcpy(dest, src)`: copies a string including its terminator; destination must have enough space.
- `strcat(dest, src)`: appends a string; destination must have enough space.

Buffer size must be checked before copying or concatenating. A string function does not automatically make an undersized destination safe.

## 2.9 Structures

A `struct` groups related members, possibly of different types.

```c
struct Student {
    int roll;
    char grade;
    float marks;
};

struct Student s = {101, 'A', 88.5f};
```

Use `.` to access a member through a structure object and `->` to access a member through a pointer to a structure.

```c
struct Student *ptr = &s;
ptr->roll = 102;     // Same as (*ptr).roll = 102;
```

Structures are especially important for linked lists and trees because a node contains data and one or more pointers to other nodes.

## 2.10 Dynamic memory allocation

Dynamic memory is requested during program execution using functions declared in `<stdlib.h>`.

| Function | Purpose |
|---|---|
| `malloc(size)` | Allocates `size` bytes; contents are uninitialized |
| `calloc(count, size)` | Allocates space for `count` objects and initializes all bytes to zero |
| `realloc(ptr, new_size)` | Resizes an allocated block; the block may move |
| `free(ptr)` | Releases a dynamically allocated block |

Example:

```c
#include <stdlib.h>

int *a = malloc(5 * sizeof *a);
if (a == NULL) {
    /* Allocation failed; handle the error. */
} else {
    for (int i = 0; i < 5; i++) {
        a[i] = i * 10;
    }
    free(a);
    a = NULL;
}
```

Safe `realloc` pattern:

```c
int *temp = realloc(a, new_count * sizeof *a);
if (temp != NULL) {
    a = temp;
} else {
    /* a still points to the original allocation. */
}
```

Common memory errors:

- **Memory leak:** allocated memory is no longer reachable and was not freed.
- **Dangling pointer:** a pointer refers to an object whose lifetime has ended or memory that has been released.
- **Double free:** the same allocated block is released more than once.
- **Invalid free:** `free` is called with a pointer that is not a valid allocation pointer (or is not `NULL`).
- **Use after free:** released memory is accessed.

## 2.11 Scope, lifetime and storage

- **Scope** tells where an identifier can be used in source code.
- **Lifetime** tells how long an object exists during execution.
- An automatic local variable normally exists during its block execution.
- A `static` local variable retains its stored value between calls and exists for the entire program execution.
- Dynamically allocated objects exist from successful allocation until they are released.

Do not confuse a variable's scope with its lifetime.

## 2.12 C concepts frequently tested in tracing questions

1. **Operator precedence:** determines how an expression is grouped; associativity resolves grouping among operators at the same precedence level. Parentheses are the clearest way to remove ambiguity.
2. **Integer versus floating-point arithmetic:** `5 / 2` is `2`, while `5.0 / 2` is `2.5`.
3. **Array indexing:** `a[i]` is equivalent to `*(a + i)` when `a` points to the first element of the array.
4. **Pointer and object types:** pointer arithmetic depends on the pointed-to type.
5. **Function calls:** each call has its own parameters and automatic local variables.
6. **Recursion:** every active call has its own local state and return point.
7. **Undefined behavior:** out-of-bounds access, dereferencing invalid pointers, and certain unsequenced modifications do not have a predictable result.

---

# 3. Recursion

## 3.1 What is recursion?

**Recursion** is a programming technique in which a function calls itself, directly or indirectly, to solve a smaller version of the same problem.

A recursive solution must contain:

1. **Base case:** the smallest case that can be answered without another recursive call.
2. **Recursive case:** the rule that reduces the current problem to one or more smaller problems.
3. **Progress:** each recursive path must eventually reach a base case.

Without a valid base case or progress toward it, the function may continue calling itself until the program runs out of call-stack space.

## 3.2 Factorial example

For a non-negative integer `n`:

\[
 n! = \begin{cases}
 1, & n = 0 \\ 
 n \times (n-1)!, & n > 0
 \end{cases}
\]

C implementation:

```c
long long factorial(int n) {
    if (n < 0) {
        return -1;              // Example error indicator
    }
    if (n == 0) {
        return 1;               // Base case
    }
    return n * factorial(n - 1);
}
```

For `factorial(4)`:

```text
factorial(4)
= 4 * factorial(3)
= 4 * 3 * factorial(2)
= 4 * 3 * 2 * factorial(1)
= 4 * 3 * 2 * 1 * factorial(0)
= 4 * 3 * 2 * 1 * 1
= 24
```

The calls are first expanded while going down the recursion, and their pending multiplications are completed while returning.

- Time complexity: `O(n)`.
- Auxiliary call-stack space: `O(n)`.

The numeric type can overflow for sufficiently large `n`; the example is for illustrating recursion, not arbitrary-precision factorials.

## 3.3 How the call stack works

A function call needs information such as its parameters, local variables and return location. Implementations commonly maintain this information in a call stack.

For `factorial(3)`, the stack grows conceptually as follows:

```text
Call phase (top shown first):

factorial(0)
factorial(1)
factorial(2)
factorial(3)

Return phase:

factorial(0) returns 1
factorial(1) returns 1 * 1 = 1
factorial(2) returns 2 * 1 = 2
factorial(3) returns 3 * 2 = 6
```

A recursive algorithm's auxiliary space depends on the maximum number of simultaneously active calls, not merely the total number of calls.

## 3.4 Sum of first n natural numbers

```c
int sum_n(int n) {
    if (n <= 0) {
        return 0;
    }
    return n + sum_n(n - 1);
}
```

For `n = 4`, the expansion is `4 + 3 + 2 + 1 + 0 = 10`.

- Time: `O(n)`.
- Stack space: `O(n)`.

## 3.5 Fibonacci numbers

One definition is:

\[
F(0)=0,\quad F(1)=1,\quad F(n)=F(n-1)+F(n-2)\; (n\ge 2)
\]

Naive recursive implementation:

```c
int fib(int n) {
    if (n <= 1) {
        return n;
    }
    return fib(n - 1) + fib(n - 2);
}
```

This function recomputes many values. Its running time grows exponentially (commonly bounded by `O(2^n)`), while the maximum call depth is `O(n)`.

For example:

```text
fib(4)
= fib(3) + fib(2)
= (fib(2) + fib(1)) + (fib(1) + fib(0))
= 3
```

The repeated call to `fib(2)` shows why the naive recursive version is inefficient. Storing previously calculated values (memoization) avoids this repeated work, but the naive function above does not do so.

## 3.6 Euclid's algorithm for GCD

The greatest common divisor satisfies:

\[
\gcd(a,b)=\gcd(b, a\bmod b),\quad \gcd(a,0)=|a|
\]

```c
int gcd(int a, int b) {
    if (b == 0) {
        return a;
    }
    return gcd(b, a % b);
}
```

Assume the inputs are non-negative integers. For `gcd(48, 18)`:

```text
 gcd(48, 18)
= gcd(18, 12)
= gcd(12, 6)
= gcd(6, 0)
= 6
```

The number of steps is `O(log(min(|a|, |b|)))` for positive inputs. Care is needed for the most negative representable integer when taking an absolute value in a fixed-width signed type.

## 3.7 Recursive binary search

Binary search requires a sorted array and a valid search interval.

```c
int binary_search(int a[], int low, int high, int key) {
    if (low > high) {
        return -1;
    }

    int mid = low + (high - low) / 2;

    if (a[mid] == key) {
        return mid;
    }
    if (key < a[mid]) {
        return binary_search(a, low, mid - 1, key);
    }
    return binary_search(a, mid + 1, high, key);
}
```

- Time: `O(log n)`.
- Recursive auxiliary space: `O(log n)` due to the call stack.
- An iterative binary search uses `O(1)` auxiliary space.

The expression `low + (high - low) / 2` is preferred over `(low + high) / 2` because it reduces the risk of overflow in the addition when the indices are non-negative and within the same integer range.

## 3.8 Direct and indirect recursion

- **Direct recursion:** a function calls itself.
- **Indirect recursion:** function A calls function B, and function B eventually calls A.

Both require a terminating condition along every possible recursive path.

## 3.9 Tail and non-tail recursion

A recursive call is in **tail position** when the function does no further work after that call returns.

Tail-recursive style:

```c
int sum_tail(int n, int acc) {
    if (n == 0) {
        return acc;
    }
    return sum_tail(n - 1, acc + n);
}
```

Non-tail-recursive style:

```c
int sum_non_tail(int n) {
    if (n == 0) {
        return 0;
    }
    return n + sum_non_tail(n - 1);
}
```

Tail-call optimization is compiler- and implementation-dependent in C; do not automatically assume that tail recursion always uses constant stack space.

## 3.10 Recursion and recurrence relations

A recurrence describes the time taken by a recursive algorithm.

| Recurrence | Typical solution | Example |
|---|---|---|
| `T(n) = T(n-1) + O(1)` | `O(n)` | Factorial / linear recursive scan |
| `T(n) = T(n-1) + O(n)` | `O(n^2)` | One linear scan at each level |
| `T(n) = T(n/2) + O(1)` | `O(log n)` | Binary-search-style reduction |
| `T(n) = 2T(n/2) + O(n)` | `O(n log n)` | Divide into two halves plus linear combine |
| `T(n) = 2T(n-1) + O(1)` | `O(2^n)` | Two recursive calls on size `n-1` |

For a recurrence of the form `T(n) = aT(n/b) + f(n)`, the Master Theorem can be useful when its conditions apply. Let `n^(log_b a)` be the comparison term:

- If `f(n)` is polynomially smaller, the recursive leaves dominate.
- If `f(n)` has the same asymptotic order, a logarithmic factor is added.
- If `f(n)` is polynomially larger and the regularity condition holds, the combine work dominates.

Do not apply the Master Theorem directly to recurrences such as `T(n)=T(n-1)+n`; use expansion or another suitable method.

## 3.11 Common recursion mistakes

- Missing a base case.
- Writing a base case that does not cover the smallest valid input.
- Making a recursive call without reducing the problem size.
- Forgetting that local variables belong to separate calls.
- Counting total calls but forgetting the maximum active depth when calculating stack space.
- Assuming all recursive algorithms are exponential.
- Assuming tail recursion is automatically optimized.

---

# 4. Arrays

## 4.1 Definition and properties

An **array** is a collection of elements of the same type stored in contiguous memory locations. Each element is accessed using an index.

Main properties:

- Direct indexing is efficient: `O(1)`.
- Elements are stored contiguously.
- A conventional fixed-size C array has a size fixed by its declaration.
- Inserting or deleting in the middle generally requires shifting elements.
- A basic array stores elements of one declared type.

## 4.2 One-dimensional array address calculation

Let:

- `B` = address of the first element,
- `w` = size in bytes of each element,
- `LB` = lower index bound,
- `i` = required index.

Then:

\[
\operatorname{LOC}(A[i])=B+(i-LB)w
\]

For a C array, the lower bound is normally `0`.

**Example:** An integer array starts at address 1000, each element occupies 4 bytes, and the required element is `A[6]`.

\[
\operatorname{LOC}(A[6])=1000+(6-0)\times 4=1024
\]

This calculation assumes the stated element size and a valid index.

## 4.3 Two-dimensional array address calculation

Suppose an array has `R` rows and `C` columns, with lower bounds `LR` and `LC`.

### Row-major order

Rows are stored one after another.

\[
\operatorname{LOC}(A[i][j])=B+\big((i-LR)C+(j-LC)\big)w
\]

### Column-major order

Columns are stored one after another.

\[
\operatorname{LOC}(A[i][j])=B+\big((j-LC)R+(i-LR)\big)w
\]

C uses row-major layout for multidimensional arrays.

**Example:** `A[3][4]` is stored in row-major order, with base address 2000 and element size 4 bytes. The address of `A[2][1]` is:

\[
2000+((2\times4)+1)\times4=2036
\]

## 4.4 Common array operations

| Operation | Typical time | Reason |
|---|---:|---|
| Read/write `A[i]` | `O(1)` | Address is calculated directly |
| Traverse all elements | `O(n)` | Each element is visited |
| Linear search | `O(n)` worst case | May inspect every element |
| Binary search on sorted array | `O(log n)` | Search interval is halved |
| Insert at end, if free capacity exists | `O(1)` | No shifting is needed |
| Insert at beginning or middle | `O(n)` | Elements may need shifting |
| Delete from end | `O(1)` | No shifting is needed |
| Delete from beginning or middle | `O(n)` | Later elements may need shifting |

For a dynamic array, an append may occasionally resize and copy the array. The amortized append cost can be `O(1)` when capacity is increased geometrically, although an individual resizing append costs `O(n)`.

## 4.5 Insertion in an array

To insert `x` at index `pos` in an array with current length `n` and available capacity:

1. Check that `pos` is between `0` and `n`.
2. Shift elements `A[n-1]` through `A[pos]` one position right.
3. Store `x` at `A[pos]`.
4. Increase the logical length by one.

Pseudocode:

```text
INSERT(A, n, capacity, pos, x)
    if n == capacity or pos < 0 or pos > n
        report failure
    for i = n - 1 down to pos
        A[i + 1] = A[i]
    A[pos] = x
    n = n + 1
```

The shift is performed from right to left so that an element is not overwritten before it is copied.

## 4.6 Deletion from an array

To delete the element at index `pos`:

1. Check that `pos` is valid (`0 <= pos < n`).
2. Shift each following element one position left.
3. Decrease the logical length by one.

Pseudocode:

```text
DELETE(A, n, pos)
    if pos < 0 or pos >= n
        report failure
    for i = pos to n - 2
        A[i] = A[i + 1]
    n = n - 1
```

The old last array cell may still contain a bit pattern, but it is outside the new logical array length.

## 4.7 Linear search

```text
LINEAR-SEARCH(A, n, key)
    for i = 0 to n - 1
        if A[i] == key
            return i
    return NOT-FOUND
```

- Works on sorted and unsorted arrays.
- Worst-case time: `O(n)`.
- Best-case time: `O(1)`.
- Auxiliary space: `O(1)`.

## 4.8 Binary search

Binary search repeatedly compares the key with the middle element of a **sorted** array.

```text
BINARY-SEARCH(A, low, high, key)
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

At each iteration, the remaining search interval is approximately half its previous size.

- Time: `O(log n)`.
- Iterative auxiliary space: `O(1)`.
- The array must be sorted according to the same ordering used by the comparison.
- If duplicates exist, ordinary binary search may return any matching occurrence; finding the first or last occurrence needs a modified condition.

## 4.9 Two-dimensional arrays and memory layout

For a C array declared as `int a[R][C]`, the element `a[i][j]` follows `i` complete rows and then `j` elements within the current row.

```text
A[2][3] in row-major order:

A[0][0] A[0][1] A[0][2]
A[1][0] A[1][1] A[1][2]

Memory order:
A[0][0], A[0][1], A[0][2], A[1][0], A[1][1], A[1][2]
```

## 4.10 Arrays: GATE points

- Indexing is `O(1)` because the address is calculated arithmetically.
- Insertion/deletion costs depend on the position, not only on the array size.
- Binary search requires sorted data; it is not a search method for an arbitrary unsorted array.
- A C array parameter is adjusted to a pointer parameter; `sizeof` inside that function does not reveal the original array length.
- For two-dimensional arrays, do not confuse `int a[R][C]` with `int **a`.
- Remember that C does not perform automatic bounds checking.

---

# 5. Stacks

## 5.1 Definition

A **stack** is a linear data structure that follows **LIFO**: Last In, First Out.

Think of a stack of plates. The plate placed on top most recently is the first plate removed.

Main operations:

- `push(x)`: insert `x` at the top.
- `pop()`: remove and return the top element.
- `peek()` or `top()`: inspect the top element without removing it.
- `isEmpty()`: check whether the stack is empty.
- `isFull()`: used by a fixed-capacity array implementation.

## 5.2 Stack using an array

Maintain an array `S[capacity]` and an integer `top`.

- Initially, `top = -1`.
- Empty condition: `top == -1`.
- Full condition: `top == capacity - 1`.

### PUSH

```text
PUSH(S, x)
    if top == capacity - 1
        report OVERFLOW
    else
        top = top + 1
        S[top] = x
```

### POP

```text
POP(S)
    if top == -1
        report UNDERFLOW
    else
        x = S[top]
        top = top - 1
        return x
```

### PEEK

```text
PEEK(S)
    if top == -1
        report EMPTY
    else
        return S[top]
```

Each successful operation takes `O(1)` time.

## 5.3 Stack using a linked list

A linked-list stack normally uses the head node as the top.

- Push: create a new node and link it before the old head.
- Pop: remove the head node and move the head to the next node.

Both operations take `O(1)` time when insertion and deletion are performed at the head.

An array stack has fixed capacity unless it is resized. A linked stack grows node by node until memory allocation fails, but each node requires pointer storage and allocation overhead.

## 5.4 Applications of stacks

1. Function calls and recursion: active function calls are managed using a call stack.
2. Parentheses matching: opening brackets are pushed; matching closing brackets pop them.
3. Expression conversion and evaluation: infix, postfix and prefix expressions.
4. Depth-first search: a stack stores the next vertices to explore.
5. Undo operations: recent actions can be reversed in last-in-first-out order.
6. Backtracking: the algorithm returns to the most recent decision point.

## 5.5 Parentheses matching

Algorithm:

1. Scan the expression from left to right.
2. Push each opening bracket `(`, `{`, `[`.
3. For a closing bracket, check that the stack is non-empty and its top is the corresponding opening bracket.
4. If not, the expression is invalid.
5. After scanning, the expression is balanced only if the stack is empty.

Time: `O(n)`. Auxiliary space: `O(n)` in the worst case.

Example:

```text
Expression:  {[a + (b * c)]}

Read '{'  -> push
Read '['  -> push
Read '('  -> push
Read ')'  -> pop '(' 
Read ']'  -> pop '['
Read '}'  -> pop '{'
Stack empty -> balanced
```

## 5.6 Infix, postfix and prefix expressions

- **Infix:** operator is between operands. Example: `A + B`.
- **Postfix (Reverse Polish):** operator follows operands. Example: `A B +`.
- **Prefix (Polish):** operator precedes operands. Example: `+ A B`.

For `(A + B) * C`:

| Form | Expression |
|---|---|
| Infix | `(A + B) * C` |
| Postfix | `A B + C *` |
| Prefix | `* + A B C` |

Postfix evaluation using a stack:

1. Scan tokens from left to right.
2. Push operands.
3. When an operator appears, pop the required operands.
4. Apply the operator in the correct order and push the result.
5. At the end, a valid single-expression evaluation leaves one result.

**Operand order matters.** For subtraction and division, if `b` is popped first and `a` second, evaluate `a - b` or `a / b`.

Example: evaluate `5 2 3 * +`.

```text
Push 5       stack: [5]
Push 2       stack: [5, 2]
Push 3       stack: [5, 2, 3]
* : 2 * 3    stack: [5, 6]
+ : 5 + 6    stack: [11]
Answer = 11
```

## 5.7 Infix-to-postfix conversion: core rules

Use an operator stack.

1. Output operands immediately.
2. Push an opening parenthesis.
3. On a closing parenthesis, pop operators to the output until the matching opening parenthesis is removed.
4. On an operator, pop operators of higher precedence; also pop operators of equal precedence when the incoming operator is left-associative. Then push the incoming operator.
5. At the end, pop remaining operators.

A common precedence order (high to low) is:

| Operator | Typical associativity |
|---|---|
| Unary operators | Depends on operator and language rules |
| `* / %` | Left-to-right |
| `+ -` | Left-to-right |
| Relational/equality operators | Left-to-right in C grammar grouping |
| `&&` | Left-to-right |
| `||` | Left-to-right |

For GATE expression-conversion problems, use the precedence and associativity explicitly stated or conventionally assumed in the question. Parentheses override ordinary precedence.

## 5.8 Stack complexity and common errors

| Operation | Array stack | Linked-list stack (head as top) |
|---|---:|---:|
| Push | `O(1)` | `O(1)` |
| Pop | `O(1)` | `O(1)` |
| Peek | `O(1)` | `O(1)` |
| Search arbitrary item | `O(n)` | `O(n)` |

Common errors:

- Confusing overflow with underflow.
- Using `top == 0` as the empty condition when the initial top is `-1`.
- Removing the bottom element instead of the top.
- Reversing the operands during postfix evaluation.
- Forgetting to check whether the stack is empty before `pop` or `peek`.

---

# 6. Queues

## 6.1 Definition

A **queue** is a linear data structure that follows **FIFO**: First In, First Out.

Think of a line of people waiting for service. The person who joins first is normally served first.

- `enqueue(x)`: insert at the rear.
- `dequeue()`: remove from the front.
- `front()`: inspect the first element.
- `isEmpty()`: test whether the queue is empty.

## 6.2 Queue using an array: linear queue

A simple linear array queue uses `front` and `rear` indexes.

A common initial state is `front = rear = -1`.

- First insertion sets both to `0`.
- Later insertions increase `rear`.
- Deletion increases `front`.

Problem: after several deletions, unused cells may remain at the beginning. A linear queue may report that the rear has reached the last index even though there are free cells before `front`. This is **false overflow** or wasted array space in the simple implementation.

## 6.3 Circular queue

A **circular queue** treats the array as circular. After the final index, the next index is `0`.

For an array of capacity `N`, with the convention that `front = rear = -1` means empty:

- Empty: `front == -1`.
- Full: `(rear + 1) % N == front`.

### ENQUEUE

```text
ENQUEUE(Q, x)
    if (rear + 1) % N == front
        report OVERFLOW
    else if front == -1
        front = rear = 0
        Q[rear] = x
    else
        rear = (rear + 1) % N
        Q[rear] = x
```

### DEQUEUE

```text
DEQUEUE(Q)
    if front == -1
        report UNDERFLOW
    else
        x = Q[front]
        if front == rear
            front = rear = -1
        else
            front = (front + 1) % N
        return x
```

Both operations take `O(1)` time.

**Example:** Let `N = 5`. Suppose `front = 3`, `rear = 4`. The next enqueue position is `(4 + 1) % 5 = 0`, so the queue wraps around to index 0 if that position is free.

## 6.4 Queue using a linked list

Maintain pointers to both the front and rear nodes.

- Enqueue at the rear: link a new node after the rear and update rear.
- Dequeue from the front: remove the front node and update front.
- If the last node is removed, set both front and rear to `NULL`.

Both operations are `O(1)` when both pointers are maintained.

## 6.5 Deque

A **double-ended queue (deque)** allows insertion and deletion at both ends.

Variants:

- Input-restricted deque: insertion is allowed at one end, deletion at both ends.
- Output-restricted deque: deletion is allowed at one end, insertion at both ends.

A deque can be implemented using a circular array or a doubly linked list.

## 6.6 Priority queue

A **priority queue** removes an element according to priority rather than strictly according to arrival time.

For example, a hospital emergency system may serve a high-priority case before a lower-priority case that arrived earlier.

A binary heap is a common implementation:

- Insert: `O(log n)`.
- Inspect highest-priority item: `O(1)`.
- Remove highest-priority item: `O(log n)`.

The exact meaning of “highest priority” depends on whether a min-priority or max-priority queue is used.

## 6.7 Queue applications

- CPU and process scheduling (depending on policy).
- Printer job handling.
- Breadth-first search (BFS).
- Request buffering and producer-consumer systems.
- Simulation of waiting lines.

## 6.8 Queue errors and GATE points

- FIFO does not mean that the values themselves must be sorted.
- In a circular queue, index movement uses modulo arithmetic.
- Do not use the linear queue's conditions for a circular queue.
- The exact full/empty conditions depend on the implementation convention. Some designs keep a separate element count or deliberately leave one cell unused.
- A linked queue needs both front and rear updates when the last element is removed.

---

# 7. Linked lists

## 7.1 Definition

A **linked list** is a collection of nodes in which each node stores data and one or more links (pointers) to other nodes.

Unlike an array, linked-list nodes do not need to be stored next to each other in memory.

A singly linked-list node in C:

```c
struct Node {
    int data;
    struct Node *next;
};
```

`head` points to the first node. An empty list has `head == NULL`.

## 7.2 Singly linked list

Each node has:

- data,
- a pointer to the next node.

The final node's `next` pointer is `NULL`.

```text
head
 |
 v
[10 | next] -> [20 | next] -> [30 | NULL]
```

### Traversal

```c
void display(struct Node *head) {
    struct Node *current = head;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
}
```

Time: `O(n)`. Auxiliary space: `O(1)` for this iterative traversal.

### Insert at the beginning

```text
new->next = head
head = new
```

Time: `O(1)`.

### Insert after a known node `p`

```text
new->next = p->next
p->next = new
```

Time: `O(1)` if `p` is already available and valid.

### Insert at the end

Without a tail pointer, traverse to the final node: `O(n)`. With a maintained tail pointer, insertion can be `O(1)`.

### Delete from the beginning

```text
if head != NULL:
    temp = head
    head = head->next
    free(temp)
```

Time: `O(1)`.

### Delete a node by value

To delete a target node in a singly linked list, retain a pointer to its predecessor so that the predecessor can bypass the target. Searching for the target takes `O(n)` in the worst case.

Special case: when the target is the first node, update `head`.

## 7.3 Doubly linked list

Each node has a pointer to both its previous and next nodes.

```c
struct DNode {
    int data;
    struct DNode *prev;
    struct DNode *next;
};
```

Advantages:

- Traversal is possible in both directions.
- Deleting a known node can be done in `O(1)` after updating its neighbors.

Disadvantages:

- Each node stores an extra pointer.
- Insertions and deletions require more link updates.

Boundary conditions at the head and tail must be handled carefully.

## 7.4 Circular linked list

In a circular linked list, the final node links back to the first node instead of storing `NULL`.

In a circular singly linked list:

```text
head -> [10] -> [20] -> [30]
          ^               |
          |_______________|
```

A traversal must stop when it reaches the starting node again. A loop that waits for `current == NULL` will not terminate in a properly circular list.

Applications include cyclic turn-taking and round-robin scheduling.

## 7.5 Complexity of common linked-list operations

| Operation | Singly linked list | Conditions |
|---|---:|---|
| Access the `k`th node | `O(n)` | Must follow links from the head |
| Search by value | `O(n)` | May inspect all nodes |
| Insert at head | `O(1)` | Head pointer available |
| Delete at head | `O(1)` | Head pointer available |
| Insert after known node | `O(1)` | Node pointer already available |
| Insert at tail | `O(n)` or `O(1)` | `O(1)` if a tail pointer is maintained |
| Delete by value | `O(n)` | Find target and predecessor |

A linked list does not provide array-style constant-time random access.

## 7.6 Reversing a singly linked list

Use three pointers: `prev`, `current` and `next`.

```c
struct Node *reverse(struct Node *head) {
    struct Node *prev = NULL;
    struct Node *current = head;

    while (current != NULL) {
        struct Node *next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    return prev;
}
```

Dry run for `10 -> 20 -> 30 -> NULL`:

| Iteration | `prev` | `current` | Action |
|---|---|---|---|
| Start | `NULL` | 10 | No links changed yet |
| 1 | 10 | 20 | 10 points to `NULL` |
| 2 | 20 | 30 | 20 points to 10 |
| 3 | 30 | `NULL` | 30 points to 20 |

New list: `30 -> 20 -> 10 -> NULL`.

- Time: `O(n)`.
- Auxiliary space: `O(1)`.

The `next` pointer must be saved before changing `current->next`; otherwise, the remaining list can be lost.

## 7.7 Detecting a cycle: Floyd's slow and fast pointer method

Use two pointers:

- `slow` moves one node per step.
- `fast` moves two nodes per step.

If they meet, a cycle exists. If `fast` reaches `NULL` (or `fast->next` is `NULL`), there is no cycle in a singly linked list.

```text
slow = head
fast = head
while fast != NULL and fast->next != NULL:
    slow = slow->next
    fast = fast->next->next
    if slow == fast:
        report cycle
report no cycle
```

- Time: `O(n)`.
- Auxiliary space: `O(1)`.

The test is pointer identity (whether the two pointers refer to the same node), not equality of the data values.

## 7.8 Arrays versus linked lists

| Feature | Array | Linked list |
|---|---|---|
| Memory layout | Contiguous | Nodes may be scattered |
| Random access | `O(1)` | `O(n)` |
| Insert at beginning | `O(n)` due to shifting | `O(1)` with head pointer |
| Delete at beginning | `O(n)` due to shifting | `O(1)` with head pointer |
| Extra pointer memory | No per-element link | One or more links per node |
| Cache locality | Usually better | Often poorer due to pointer traversal |
| Capacity | Fixed for a fixed array; dynamic arrays resize | Grows node by node, limited by available memory |

## 7.9 Common linked-list mistakes

- Losing the remaining list by updating a pointer in the wrong order.
- Forgetting the empty-list case.
- Forgetting the one-node case.
- Failing to update `head` or `tail` after insertion/deletion.
- Not freeing a removed dynamically allocated node.
- Using `current != NULL` as the stop condition for a circular list.
- Comparing node values instead of node addresses in cycle detection.

---

# 8. Trees

## 8.1 What is a tree?

A **tree** is a hierarchical data structure consisting of nodes connected by edges. In a rooted tree, one node is selected as the **root**.

A tree is useful for representing hierarchical relationships such as file systems, organization charts and expression structures.

## 8.2 Basic terminology

Consider this tree:

```text
          A
        /   \
       B     C
      / \     \
     D   E     F
```

- **Node:** an element of the tree, such as `A` or `B`.
- **Root:** the top node (`A`).
- **Edge:** a connection between two nodes.
- **Parent:** the node directly above another node (`B` is the parent of `D`).
- **Child:** a node directly below another node (`D` is a child of `B`).
- **Siblings:** nodes with the same parent (`B` and `C`).
- **Leaf/external node:** a node with no children (`D`, `E`, `F`).
- **Internal node:** a node with at least one child (`A`, `B`, `C`).
- **Ancestor:** any node on the path from the root to a given node.
- **Descendant:** any node below a given node.
- **Subtree:** a node together with all its descendants.
- **Depth of a node:** number of edges from the root to that node; root depth is 0.
- **Height of a node:** number of edges on the longest downward path from that node to a leaf.
- **Height of a tree:** height of its root.

Some textbooks count height in nodes or define the height of an empty tree differently. Always check the convention used in a question. This guide measures height in edges, so a single-node tree has height 0.

## 8.3 General tree properties

For a non-empty tree with `n` nodes:

- Number of edges = `n - 1`.
- There is exactly one simple path between any two nodes in a tree.
- A tree is connected and has no cycles.

For a rooted tree, every node except the root has exactly one parent.

## 8.4 Binary tree

A **binary tree** is a rooted tree in which each node has at most two children, usually called the left child and right child.

A binary tree is not necessarily a binary search tree. A general binary tree has no ordering rule between its node values.

### Types of binary trees

1. **Full (proper/strict) binary tree:** every node has either 0 or 2 children.
2. **Perfect binary tree:** every internal node has exactly 2 children and all leaves are at the same level.
3. **Complete binary tree:** every level is completely filled except possibly the last, and the last level is filled from left to right.
4. **Skewed/degenerate binary tree:** each internal node has only one child, producing a chain.

These terms are not interchangeable. In particular, every perfect binary tree is complete, but a complete binary tree need not be perfect.

## 8.5 Important binary-tree properties

Assume the root is at level 0.

- Maximum number of nodes at level `l`: `2^l`.
- Maximum number of nodes in a binary tree of height `h` edges:

\[
1+2+4+\cdots+2^h=2^{h+1}-1
\]

- Minimum number of nodes in a non-empty binary tree of height `h` edges: `h+1` (a chain).
- For a perfect binary tree of height `h`:
  - Total nodes: `2^(h+1)-1`.
  - Leaf nodes: `2^h`.
  - Internal nodes: `2^h-1`.
- For a full binary tree, if `n0` is the number of leaves and `n2` the number of nodes with two children:

\[
n_0=n_2+1
\]

### Derivation of `n0 = n2 + 1`

Let `n1` be the number of nodes with one child. The total number of nodes is:

\[
n=n_0+n_1+n_2
\]

Every node except the root has one incoming edge, so the number of edges is `n-1`. Counting edges by the outgoing children of nodes gives:

\[
n-1=n_1+2n_2
\]

Substitute `n`:

\[
n_0+n_1+n_2-1=n_1+2n_2
\]

Therefore, `n0 = n2 + 1`.

## 8.6 Binary-tree representation

### Linked representation

```c
struct TreeNode {
    int data;
    struct TreeNode *left;
    struct TreeNode *right;
};
```

Each node stores its value and links to its left and right child. A missing child is represented by `NULL`.

### Array representation

For a complete binary tree stored in a zero-indexed array:

- Parent of index `i` (when `i > 0`): `floor((i - 1) / 2)`.
- Left child: `2i + 1`.
- Right child: `2i + 2`.

For a one-indexed array:

- Parent: `floor(i / 2)`.
- Left child: `2i`.
- Right child: `2i + 1`.

Array representation is efficient for complete or nearly complete trees. It can waste a large amount of space for a sparse or highly skewed tree.

## 8.7 Tree traversals

A traversal visits every node in a specified order.

Use this tree:

```text
          A
        /   \
       B     C
      / \   / \
     D   E F   G
```

### Preorder: Root, Left, Right (NLR)

```text
PREORDER(node)
    if node == NULL: return
    visit(node)
    PREORDER(node.left)
    PREORDER(node.right)
```

Output: `A B D E C F G`.

### Inorder: Left, Root, Right (LNR)

```text
INORDER(node)
    if node == NULL: return
    INORDER(node.left)
    visit(node)
    INORDER(node.right)
```

Output: `D B E A F C G`.

For a binary search tree, inorder traversal visits values in non-decreasing order (strictly increasing when keys are distinct).

### Postorder: Left, Right, Root (LRN)

```text
POSTORDER(node)
    if node == NULL: return
    POSTORDER(node.left)
    POSTORDER(node.right)
    visit(node)
```

Output: `D E B F G C A`.

### Level-order traversal

Visit nodes level by level, from left to right at each level. A queue is used.

Output: `A B C D E F G`.

For a tree with `n` nodes, each traversal takes `O(n)` time. Recursive depth-first traversals use `O(h)` call-stack space, where `h` is the tree height. Level-order traversal uses a queue whose size can be `O(n)` in the worst case.

## 8.8 Recursive tree algorithms

### Count nodes

```text
COUNT(node)
    if node == NULL: return 0
    return 1 + COUNT(node.left) + COUNT(node.right)
```

Time: `O(n)`. Recursive stack: `O(h)`.

### Find height (height in edges)

```text
HEIGHT(node)
    if node == NULL: return -1
    return 1 + max(HEIGHT(node.left), HEIGHT(node.right))
```

With this convention, a leaf has height 0 and an empty tree has height -1.

Time: `O(n)`. Recursive stack: `O(h)`.

### Count leaves

```text
COUNT-LEAVES(node)
    if node == NULL: return 0
    if node.left == NULL and node.right == NULL: return 1
    return COUNT-LEAVES(node.left) + COUNT-LEAVES(node.right)
```

## 8.9 Expression trees

An expression tree stores operators in internal nodes and operands in leaves.

For `(a + b) * c`:

```text
          *
        /   \
       +     c
      / \
     a   b
```

- Preorder gives prefix: `* + a b c`.
- Inorder gives infix: `(a + b) * c` (parentheses may be needed to preserve grouping).
- Postorder gives postfix: `a b + c *`.

## 8.10 Common tree mistakes

- Confusing a binary tree with a binary search tree.
- Mixing up preorder, inorder and postorder.
- Using the one-indexed child formulas with a zero-indexed array.
- Forgetting that height may be measured in edges or nodes.
- Assuming a complete tree must be perfect.
- Forgetting that recursive traversal stack space depends on tree height: a skewed tree can have height `O(n)`.

---

# 9. Binary search trees

## 9.1 Definition and ordering property

A **binary search tree (BST)** is a binary tree in which, for every node:

- all keys in its left subtree are less than the node's key,
- all keys in its right subtree are greater than the node's key,
- and both subtrees are themselves BSTs.

This guide assumes distinct keys. If duplicates are allowed, the implementation must define a consistent duplicate policy (for example, always place equal keys on one chosen side).

Example:

```text
          50
        /    \
       30     70
      / \    / \
     20 40  60 80
```

For every node, the ordering property must hold throughout its entire left and right subtrees, not merely for its immediate children.

## 9.2 Searching in a BST

```text
BST-SEARCH(root, key)
    current = root
    while current != NULL
        if key == current.key
            return current
        else if key < current.key
            current = current.left
        else
            current = current.right
    return NOT-FOUND
```

At each step, one subtree is eliminated from consideration.

- Time: `O(h)`, where `h` is the tree height.
- Balanced / logarithmic-height tree: `O(log n)`.
- Worst-case skewed tree: `O(n)`.
- Iterative auxiliary space: `O(1)`.

## 9.3 Insertion in a BST

Start at the root and follow the search path. Insert the new key at the first `NULL` child position where the ordering property permits it.

Example: insert `65` into the earlier tree.

```text
65 > 50  -> move right to 70
65 < 70  -> move left to 60
65 > 60  -> insert as right child of 60
```

Insertion takes `O(h)` time. It does not automatically keep the tree balanced.

## 9.4 Deletion in a BST

There are three cases.

### Case 1: deleting a leaf

Remove the leaf and set its parent's corresponding link to `NULL`.

### Case 2: deleting a node with one child

Connect the parent directly to the node's only child. The removed node is bypassed.

### Case 3: deleting a node with two children

A common method is:

1. Find the node's **inorder successor**, the smallest node in its right subtree.
2. Copy or move the successor's key into the node being deleted.
3. Delete the successor from its old position. The successor has no left child, so its removal is simpler (it may have a right child).

The inorder predecessor (largest node in the left subtree) can be used instead.

Each case takes `O(h)` time when locating the target and successor/predecessor.

## 9.5 Minimum, maximum and inorder successor

- Minimum: follow left links until no left child exists.
- Maximum: follow right links until no right child exists.
- Inorder successor of a node:
  - If it has a right subtree, take the minimum of that right subtree.
  - Otherwise, move upward until reaching an ancestor for which the node lies in that ancestor's left subtree.

The second rule requires parent pointers or an appropriate search path/stack.

## 9.6 BST traversal

Inorder traversal of the example tree:

```text
20, 30, 40, 50, 60, 70, 80
```

The sorted order is a direct consequence of the BST ordering property.

## 9.7 BST complexity

| Operation | Time in terms of height `h` | Balanced tree | Skewed worst case |
|---|---:|---:|---:|
| Search | `O(h)` | `O(log n)` | `O(n)` |
| Insert | `O(h)` | `O(log n)` | `O(n)` |
| Delete | `O(h)` | `O(log n)` | `O(n)` |
| Find minimum/maximum | `O(h)` | `O(log n)` | `O(n)` |
| Inorder traversal | `O(n)` | `O(n)` | `O(n)` |

A plain BST can become skewed if keys are inserted in sorted order. Self-balancing trees are designed to control height, but their detailed balancing rules are outside the topic list here.

## 9.8 Common BST traps

- A BST's left subtree must contain keys smaller than the node and its right subtree larger (under the distinct-key convention).
- Checking only parent-child comparisons is insufficient; the full subtree range must be respected.
- Inorder traversal is sorted; preorder and postorder are not generally sorted.
- BST operations are not always `O(log n)`. Their time depends on height.
- Deleting a two-child node does not mean simply deleting it; an inorder successor or predecessor is used to preserve order.

---

# 10. Binary heaps

## 10.1 Definition

A **binary heap** is a complete binary tree that satisfies a heap-order property.

Two common types:

- **Max-heap:** every parent key is greater than or equal to its children's keys. The maximum is at the root.
- **Min-heap:** every parent key is less than or equal to its children's keys. The minimum is at the root.

A heap is not a BST. A heap guarantees parent-child order, not complete left-subtree/right-subtree ordering.

## 10.2 Array representation

A binary heap is commonly stored in an array because it is a complete binary tree.

For zero-based indexing:

- Parent of `i` (`i > 0`): `floor((i - 1) / 2)`.
- Left child: `2i + 1`.
- Right child: `2i + 2`.

For one-based indexing:

- Parent: `floor(i / 2)`.
- Left child: `2i`.
- Right child: `2i + 1`.

No explicit child pointers are required.

## 10.3 Insertion into a max-heap

1. Place the new key at the next free array position to preserve completeness.
2. Compare it with its parent.
3. If it is larger than the parent, swap them.
4. Continue upward until the heap property is restored or the root is reached.

This is called **sift up**, **bubble up** or **heapify up**.

Time: `O(log n)` because the height of a complete binary tree is `O(log n)`.

## 10.4 Delete maximum from a max-heap

1. Save the root value (the maximum).
2. Move the final array element to the root.
3. Remove the final array position.
4. Compare the new root with its children.
5. Swap it with the larger child if the heap property is violated.
6. Continue downward until the heap property holds.

This is **sift down** or **heapify down**.

Time: `O(log n)`.

For a min-heap, delete-min follows the same procedure but uses the smaller child.

## 10.5 Build a heap

There are two common ways to create a heap from `n` values:

1. Insert values one at a time: worst-case total `O(n log n)`.
2. Put the values into an array and apply bottom-up heap construction: `O(n)`.

### Why bottom-up build-heap is `O(n)`

Most nodes are near the leaves and need very little sift-down work. Only a small number of nodes are high in the tree and can move many levels. Summing the work over all nodes gives linear total work, even though one sift-down can take `O(log n)`.

Bottom-up pseudocode for a max-heap with zero-based array indexing:

```text
BUILD-MAX-HEAP(A, n)
    for i = floor(n / 2) - 1 down to 0
        SIFT-DOWN(A, i, n)
```

The last internal node is at index `floor(n/2)-1`; nodes after it are leaves and already satisfy the heap property.

## 10.6 Heap sort

Heap sort for ascending order using a max-heap:

1. Build a max-heap.
2. Swap the root (maximum) with the last element in the heap.
3. Reduce the heap size by one.
4. Sift down the new root.
5. Repeat until the heap size is one.

Complexities:

- Build heap: `O(n)`.
- Repeated extraction: `O(n log n)` total.
- Overall time: `O(n log n)` in best, average and worst cases.
- Auxiliary space: `O(1)` for the standard in-place iterative implementation.
- Standard heap sort is not stable.

## 10.7 Heap operation summary

| Operation | Time |
|---|---:|
| Find maximum in max-heap / minimum in min-heap | `O(1)` |
| Insert | `O(log n)` |
| Delete root | `O(log n)` |
| Build heap bottom-up | `O(n)` |
| Search for arbitrary key | `O(n)` |
| Heap sort | `O(n log n)` |

An arbitrary key is not generally found in `O(log n)` because the heap does not provide the full BST ordering property.

## 10.8 Heap versus BST

| Feature | Binary heap | Binary search tree |
|---|---|---|
| Shape | Complete binary tree | No fixed shape rule in an ordinary BST |
| Ordering | Parent-child heap order | Every left-subtree key is smaller; every right-subtree key is larger (distinct-key case) |
| Root | Global min or max | No guaranteed global min or max at root |
| Find min/max | `O(1)` for the corresponding heap type | `O(h)` by following left/right links |
| Search arbitrary key | `O(n)` | `O(h)` |
| Insert | `O(log n)` | `O(h)` |
| Delete root / chosen key | Root removal `O(log n)` | Chosen-key deletion `O(h)` |
| Common use | Priority queues and heap sort | Ordered search and ordered traversal |

## 10.9 Common heap mistakes

- Assuming every left-subtree key is smaller than every right-subtree key.
- Mixing zero-based and one-based array formulas.
- Sifting up during root deletion instead of sifting down.
- Choosing the wrong child while sifting down (for a max-heap, compare with the larger child).
- Claiming that bottom-up build-heap is `O(n log n)`; its tight bound is `O(n)`.
- Claiming that an arbitrary heap search is `O(log n)`.

---

# 11. Graphs

## 11.1 Definition

A **graph** is a data structure consisting of:

- a set of vertices (or nodes), and
- a set of edges connecting pairs of vertices.

It is commonly written as `G = (V, E)`, where `V` is the vertex set and `E` is the edge set.

Graphs represent road networks, social networks, communication networks, dependencies and many other relationships.

## 11.2 Types of graphs

- **Undirected graph:** an edge `{u, v}` has no direction.
- **Directed graph (digraph):** an edge `(u, v)` goes from `u` to `v`.
- **Weighted graph:** edges have associated weights or costs.
- **Unweighted graph:** edges are treated as having equal cost for basic path-length purposes.
- **Simple graph:** no self-loops and no parallel edges.
- **Connected undirected graph:** there is a path between every pair of vertices.
- **Disconnected graph:** at least one pair of vertices has no path between them.
- **Complete undirected graph:** every pair of distinct vertices is connected by an edge.
- **DAG:** directed acyclic graph; a directed graph with no directed cycle.

## 11.3 Basic graph terminology

- **Adjacent vertices:** vertices joined by an edge.
- **Degree of a vertex in an undirected graph:** number of incident edges (a self-loop, if permitted, contributes 2).
- **Indegree:** number of incoming edges to a vertex in a directed graph.
- **Outdegree:** number of outgoing edges from a vertex in a directed graph.
- **Path:** a sequence of vertices connected by edges.
- **Cycle:** a path that starts and ends at the same vertex, subject to the relevant definition of a simple cycle.
- **Length of a path:** number of edges in it (unless a weighted length is specified).
- **Connected component:** a maximal connected part of an undirected graph.
- **Isolated vertex:** a vertex with degree 0.
- **Self-loop:** an edge from a vertex to itself.
- **Parallel edges:** multiple edges between the same pair of vertices; these are excluded in a simple graph.

### Degree-sum properties

For an undirected graph:

\[
\sum_{v\in V}\deg(v)=2|E|
\]

Each edge contributes 1 to the degree of each of its two endpoints.

For a directed graph:

\[
\sum_{v\in V}\operatorname{indeg}(v)=|E|,
\qquad
\sum_{v\in V}\operatorname{outdeg}(v)=|E|
\]

Every directed edge has one tail and one head.

For a simple undirected graph with `V` vertices, the maximum number of edges is:

\[
\frac{V(V-1)}{2}
\]

For a simple directed graph without self-loops, the maximum number of directed edges is `V(V-1)`.

## 11.4 Graph representation

### Adjacency matrix

For a graph with `V` vertices, an adjacency matrix is a `V x V` matrix.

- In an unweighted graph, `A[i][j]` is 1 when an edge exists and 0 otherwise.
- In a weighted graph, the cell can store the edge weight; a separate marker is needed to distinguish “no edge” from a valid weight such as zero.

For an undirected graph, the matrix is symmetric.

Complexities:

- Space: `O(V^2)`.
- Check whether a particular edge exists: `O(1)`.
- List all neighbors of one vertex: `O(V)`.

### Adjacency list

For each vertex, store a list of its neighbors.

- For an undirected graph, each edge is normally stored in the lists of both endpoints.
- For a directed graph, store outgoing neighbors (or use a separate incoming representation when needed).

Complexities:

- Space: `O(V + E)` for a standard representation.
- Iterate over the neighbors of `u`: `O(degree(u))`.
- Check whether a specific edge exists: up to `O(degree(u))` with an unsorted list; other auxiliary structures may improve lookup.

### Matrix versus list

| Feature | Adjacency matrix | Adjacency list |
|---|---|---|
| Space | `O(V^2)` | `O(V+E)` |
| Best suited to | Dense graphs / frequent edge tests | Sparse graphs / neighbor traversal |
| Check edge | `O(1)` | `O(degree(u))` in a basic list |
| Iterate neighbors | `O(V)` | `O(degree(u))` |

## 11.5 Breadth-first search (BFS)

**BFS** explores a graph level by level from a source vertex. It uses a queue.

Pseudocode for a graph represented by adjacency lists:

```text
BFS(G, source)
    mark source visited
    enqueue(source)

    while queue is not empty
        u = dequeue()
        process(u)
        for each neighbor v of u
            if v is not visited
                mark v visited
                enqueue(v)
```

Mark a vertex as visited when it is enqueued. This prevents it from being enqueued repeatedly through different incoming edges.

Complexity with adjacency lists:

- Time: `O(V + E)` for a full traversal of the reachable part; `O(V+E)` for a full graph traversal including repeated starts for disconnected components.
- Extra space: `O(V)` for visited state and queue.

BFS finds shortest paths measured by number of edges in an unweighted graph (or when all edges have equal cost). Ordinary BFS does not solve the general weighted shortest-path problem.

## 11.6 Depth-first search (DFS)

**DFS** explores as far as possible along one path before backtracking. It can be implemented recursively or with an explicit stack.

Recursive pseudocode:

```text
DFS(G, u)
    mark u visited
    process(u)
    for each neighbor v of u
        if v is not visited
            DFS(G, v)
```

Complexity with adjacency lists:

- Time: `O(V + E)` for a full graph traversal.
- Extra space: `O(V)` in the worst case for visited state plus recursion/stack.

The precise visit order depends on the order in which a vertex's neighbors are stored or examined. If a problem specifies an adjacency order, follow it exactly.

## 11.7 BFS versus DFS

| Feature | BFS | DFS |
|---|---|---|
| Main structure | Queue | Stack or recursion |
| Exploration | Level by level | Deep path, then backtrack |
| Shortest path in an unweighted graph | Yes, by edge count | Not guaranteed |
| Typical uses | Unweighted shortest paths, levels, reachability | Cycle checks, components, structural exploration |
| Adjacency-list time | `O(V+E)` | `O(V+E)` |
| Extra storage | `O(V)` | `O(V)` worst case |

## 11.8 Traversing a disconnected graph

Starting BFS or DFS from one source visits only vertices reachable from that source. To visit every vertex in a disconnected graph:

```text
for each vertex v in V
    if v is not visited
        run BFS(G, v)       // or DFS(G, v)
```

Each new traversal starts a new connected component in an undirected graph.

## 11.9 Topological ordering of a DAG

A **topological ordering** is a linear ordering of vertices in a directed acyclic graph such that for every directed edge `u -> v`, `u` appears before `v`.

A topological ordering exists if and only if the directed graph is acyclic.

Kahn's algorithm:

1. Compute the indegree of every vertex.
2. Enqueue all vertices with indegree 0.
3. Repeatedly remove one such vertex and append it to the order.
4. For each outgoing edge, reduce the destination's indegree; enqueue it if its indegree becomes 0.
5. If all vertices are output, the graph is a DAG. If fewer than `V` vertices are output, a directed cycle exists.

Time with adjacency lists: `O(V + E)`.

## 11.10 Common graph mistakes

- Treating a directed edge as if it worked in both directions.
- Forgetting that an undirected edge is typically stored twice in an adjacency list.
- Using `O(V^2)` as the adjacency-list traversal complexity for every graph.
- Assuming BFS finds shortest weighted paths for arbitrary weights.
- Assuming a traversal from one source visits a disconnected graph completely.
- Marking vertices visited too late and inserting duplicates into a BFS queue.
- Assuming BFS/DFS visit order is unique without a specified neighbor order.
- Confusing a cycle with a path; a DAG has no directed cycle.

---

# 12. Comparisons and complexity summary

## 12.1 Linear data structures

| Structure | Ordering rule | Efficient operations | Main limitation |
|---|---|---|---|
| Array | Position/index | Random access `O(1)` | Middle insertion/deletion needs shifting |
| Stack | LIFO | Push/pop at top `O(1)` | Access is restricted to the top |
| Queue | FIFO | Enqueue/dequeue `O(1)` with suitable implementation | Access is restricted to ends |
| Linked list | Link order | Insert/delete at a known position/node | No direct random access |

## 12.2 Tree structures

| Structure | Key property | Useful for |
|---|---|---|
| Binary tree | At most two children per node | Hierarchies and expression structures |
| BST | Left keys smaller, right keys larger (distinct keys) | Ordered searching |
| Binary heap | Complete shape plus heap order | Priority queues and heap sort |

## 12.3 Operation complexity table

Assume standard implementations and `n` stored elements. For BST, `h` means actual tree height.

| Operation | Array | Linked list | Stack | Queue | BST | Binary heap |
|---|---:|---:|---:|---:|---:|---:|
| Access by index | `O(1)` | `O(n)` | Not general | Not general | Not general | `O(1)` to read a known array position, not ordered search |
| Search arbitrary value | `O(n)` | `O(n)` | `O(n)` | `O(n)` | `O(h)` | `O(n)` |
| Insert at front | `O(n)` | `O(1)` | Push if top is front | Not normal queue operation | `O(h)` for key insertion | Not a general heap operation |
| Insert at end | `O(1)` if capacity available | `O(n)` or `O(1)` with tail | Not normal stack operation | Enqueue `O(1)` | `O(h)` for key insertion | Insert `O(log n)` |
| Remove next/top item | Position-dependent | Position-dependent | Pop `O(1)` | Dequeue `O(1)` | Delete chosen key `O(h)` | Remove root `O(log n)` |
| Inspect priority item | N/A | N/A | Top `O(1)` | Front `O(1)` | Min/max `O(h)` | Root `O(1)` |

The table compares typical operations, not every possible implementation. A dynamic array, a circular queue, a list with a tail pointer, and a balanced search tree have different implementation details.

## 12.4 Important time and space facts

| Algorithm / operation | Time | Auxiliary space |
|---|---:|---:|
| Array indexing | `O(1)` | `O(1)` |
| Array traversal | `O(n)` | `O(1)` iterative |
| Linear search | `O(n)` worst | `O(1)` |
| Binary search | `O(log n)` | `O(1)` iterative; `O(log n)` recursive |
| Stack push/pop | `O(1)` | `O(1)` per operation, excluding stored data |
| Queue enqueue/dequeue | `O(1)` | `O(1)` per operation, excluding stored data |
| Linked-list traversal | `O(n)` | `O(1)` iterative |
| Linked-list reversal | `O(n)` | `O(1)` iterative |
| Tree traversal | `O(n)` | `O(h)` recursive DFS; level-order queue up to `O(n)` |
| BST search/insert/delete | `O(h)` | Depends on iterative/recursive implementation |
| Heap insertion/delete-root | `O(log n)` | `O(1)` iterative |
| Bottom-up build-heap | `O(n)` | `O(1)` in-place |
| BFS/DFS with adjacency list | `O(V+E)` | `O(V)` |

---

# 13. GATE problem-solving approach and common traps

## 13.1 A reliable method for code-tracing questions

1. Write down the initial values of every variable.
2. Identify the exact order in which statements execute.
3. For pointers, distinguish the pointer variable from the object it points to.
4. For arrays, record the index and value separately.
5. For recursion, draw the call sequence and return sequence separately.
6. For stack/queue questions, draw the contents after every operation.
7. For linked lists, draw arrows and update them in the exact order of the code.
8. For trees and heaps, draw the structure after each insertion/deletion.
9. For graphs, write the adjacency order and visited state; traversal order can depend on neighbor order.
10. Check boundary cases such as empty, one element, full capacity and absent key.

## 13.2 Common traps by topic

| Topic | Trap | Correct approach |
|---|---|---|
| C | Assuming all expressions have a simple left-to-right evaluation order | Apply precedence, associativity and sequencing rules; flag undefined behavior where relevant |
| C pointers | Treating pointer arithmetic as byte-by-byte movement | Movement is scaled by the pointed-to type |
| C arrays | Assuming array bounds are checked | Check indexes explicitly |
| Recursion | Counting only the number of calls | Analyze work per call and maximum active depth |
| Arrays | Applying binary search to unsorted data | Confirm sorted order first |
| Stack | Reversing LIFO | The most recently pushed item is removed first |
| Queue | Reversing FIFO | The earliest enqueued item is removed first |
| Circular queue | Forgetting wrap-around | Use modulo arithmetic and the implementation's full/empty rule |
| Linked list | Losing the next node during link changes | Save `next` before changing the link |
| Tree | Mixing height conventions | State whether height is counted in edges or nodes |
| BST | Assuming all operations are logarithmic | Express time in terms of height `h` |
| Heap | Treating a heap like a BST | Only parent-child order is guaranteed |
| Graph | Missing disconnected components | Start a traversal from every unvisited vertex |

## 13.3 How to calculate traversal complexity

For an adjacency-list graph traversal:

- Each vertex is marked/processed at most a constant number of times: total `O(V)`.
- Across the traversal, adjacency lists account for `O(E)` edge examinations (up to a constant-factor difference for undirected graphs).
- Total: `O(V + E)`.

For an adjacency matrix, checking the neighbors of each vertex requires scanning a row of length `V`. Across all vertices, this is `O(V^2)`.

## 13.4 Edge cases worth testing

- Empty array, list, stack, queue, tree or graph.
- One-element structure.
- Insertion into an empty linked list.
- Deletion of the only linked-list node.
- Circular queue wrapping from the last index to index 0.
- Duplicate values in an array or BST (the BST duplicate policy must be known).
- A completely skewed BST or tree.
- A graph with isolated vertices or multiple components.
- Self-loops and parallel edges if the graph definition permits them.
- Recursive input at the base case and just above the base case.

---

# 14. Practice questions

**Instructions:** Attempt these questions without looking at the answer key. Unless stated otherwise, assume valid input, zero-based array indexing, distinct BST keys, and standard implementations described in this guide. Questions are newly written for practice and are not claimed to be previous-year GATE questions.

## Section A — Multiple-choice questions (MCQ)

### Q1. C arrays

For `int a[10];`, which expression accesses the same element as `a[4]`?

A. `*(a + 4)`  
B. `*a + 4`  
C. `&a + 4`  
D. `*(a) + 4`

### Q2. C function arguments

C uses which parameter-passing mechanism?

A. Pass-by-reference for all arguments  
B. Pass-by-value  
C. Pass-by-name  
D. Copy-on-write for all arguments

### Q3. Recursion

For the recursive function `f(n) { if (n == 0) return 0; return 1 + f(n-1); }`, what is its time complexity for `n >= 0`?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(2^n)`

### Q4. Array complexity

What is the worst-case time complexity of inserting an element at index 0 in an array of `n` elements, assuming the array has free capacity?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n log n)`

### Q5. Binary search

Which condition is essential for ordinary binary search?

A. The array must contain distinct values.  
B. The array must be sorted according to the search comparison.  
C. The array size must be a power of two.  
D. The key must be present.

### Q6. Stack

A stack receives `push(3)`, `push(5)`, `pop()`, `push(7)`, `pop()`. What value is returned by the second `pop()`?

A. 3  
B. 5  
C. 7  
D. The stack is empty

### Q7. Queue

A queue receives `enqueue(4)`, `enqueue(8)`, `dequeue()`, `enqueue(9)`. What is at the front?

A. 4  
B. 8  
C. 9  
D. Empty

### Q8. Linked list

Which operation is `O(1)` in a singly linked list when only a head pointer is maintained?

A. Search for a value  
B. Access the 10th node  
C. Insert at the beginning  
D. Insert at the end

### Q9. Tree traversal

Which traversal of a BST produces keys in non-decreasing order?

A. Preorder  
B. Inorder  
C. Postorder  
D. Level-order

### Q10. BST complexity

A BST is formed by inserting `10, 20, 30, 40` in that order. What is the worst-case search time for this tree with `n` nodes?

A. `O(1)`  
B. `O(log n)`  
C. `O(n)`  
D. `O(n log n)`

### Q11. Heap

In a max-heap, which value is guaranteed to be at the root?

A. Minimum value  
B. Maximum value  
C. Median value  
D. Smallest leaf value

### Q12. Graph representation

Which representation usually requires `O(V^2)` space?

A. Adjacency list  
B. Adjacency matrix  
C. Edge list  
D. BFS queue

## Section B — Multiple-select questions (MSQ)

### Q13. Recursion

Select all correct statements.

A. Every recursive function must have a terminating condition along every recursive path.  
B. Recursive calls commonly use call-stack space.  
C. Every recursive algorithm has `O(n)` time complexity.  
D. Maximum recursion depth helps determine auxiliary stack space.

### Q14. Arrays and linked lists

Select all correct statements.

A. Array indexing is `O(1)` in the usual RAM model.  
B. A singly linked list supports `O(1)` random access by position.  
C. Insertion at the head of a singly linked list is `O(1)`.  
D. Inserting at the beginning of an array usually requires shifting elements.

### Q15. Binary trees

Select all correct statements.

A. Every perfect binary tree is complete.  
B. Every complete binary tree is perfect.  
C. A full binary tree has either zero or two children at every node.  
D. A binary tree node can have at most two children.

### Q16. Binary heaps

Select all correct statements about a max-heap.

A. The root contains a maximum key.  
B. The tree is complete.  
C. Every node's left subtree contains only keys smaller than every key in its right subtree.  
D. Insertion takes `O(log n)` time.

### Q17. Graph traversal

Select all correct statements.

A. BFS uses a queue in its standard implementation.  
B. DFS can be implemented recursively.  
C. BFS gives shortest paths by number of edges in an unweighted graph.  
D. A traversal started at one vertex must visit every vertex of a disconnected graph.

## Section C — Numerical answer type (NAT)

### Q18. Array address

An integer array has base address 1200, each element occupies 4 bytes, and indexing starts at 0. Find the address of `A[9]`.

### Q19. Two-dimensional address

A C array `A[4][5]` is stored in row-major order. Its base address is 1000 and each element occupies 2 bytes. Find the address of `A[2][3]`.

### Q20. Perfect binary tree

A perfect binary tree has height 4, where height is measured in edges and the root is at level 0. Find the total number of nodes.

### Q21. Full binary tree

A full binary tree has 12 internal nodes. How many leaves does it have?

### Q22. Circular queue

A circular queue has capacity 8. Its rear index is 6. Find the next index calculated by `(rear + 1) % 8`.

### Q23. Heap array

In a zero-indexed heap, find the left-child index of the node at index 7.

### Q24. Graph degree sum

An undirected graph has 7 edges. What is the sum of the degrees of all vertices?

## Section D — Short answer and application questions

### Q25. C pointer tracing

What is printed?

```c
int x = 10;
int *p = &x;
*p = *p + 5;
printf("%d", x);
```

### Q26. Recursion tracing

Find the output of `sum(4)`.

```c
int sum(int n) {
    if (n == 0) return 0;
    return n + sum(n - 1);
}
```

### Q27. Stack trace

An initially empty stack performs:

```text
push(2), push(4), push(6), pop(), push(8), pop(), peek()
```

What does `peek()` return, and what remains in the stack from bottom to top?

### Q28. Linked-list reversal

Write the three-pointer idea used to reverse a singly linked list iteratively. State its time and auxiliary-space complexity.

### Q29. BST construction

Insert `40, 20, 60, 10, 30, 50, 70` into an empty BST. Give its inorder traversal and identify the root's inorder successor.

### Q30. Heap operation

A max-heap array is `[50, 30, 40, 10, 20, 35]`. Delete the maximum and show the resulting max-heap array using the standard move-last-to-root and sift-down method.

### Q31. BFS trace

Consider an undirected graph with adjacency order:

```text
A: B, C
B: A, D, E
C: A, F
D: B
E: B, F
F: C, E
```

Give the BFS order starting at `A`, marking a vertex visited when it is enqueued.

### Q32. Complexity comparison

A problem requires frequent retrieval of the current largest item and frequent insertion of new items. Which is more suitable: an unsorted array, a max-heap, or an ordinary BST? Explain using operation complexities.

---

# 15. Detailed answer key

## Q1. Answer: A

For a valid array index, `a[i]` is defined as `*(a + i)`. Therefore, `a[4]` and `*(a + 4)` access the same element. `*a + 4` means the first element's value plus 4, not the fifth element.

## Q2. Answer: B

C passes arguments by value. When the argument is a pointer, the pointer value (address) is copied. The called function can still modify the pointed-to object through that copied address.

## Q3. Answer: C

The function makes one recursive call with `n-1` and performs constant work. Its recurrence is `T(n) = T(n-1) + O(1)`, with a constant base case. There are `n+1` calls, so time is `O(n)`.

## Q4. Answer: C

Inserting at index 0 shifts all `n` current elements one position to the right. The number of assignments grows linearly, so the worst-case time is `O(n)`.

## Q5. Answer: B

Binary search decides which half to discard based on the ordering of the middle element. That decision is valid only when the array is sorted according to the comparison. Distinct values, a power-of-two length and the presence of the key are not required.

## Q6. Answer: C

Trace:

```text
push(3) -> [3]
push(5) -> [3, 5]
pop()   -> returns 5; stack [3]
push(7) -> [3, 7]
pop()   -> returns 7; stack [3]
```

The second `pop()` returns `7`.

## Q7. Answer: B

Trace:

```text
enqueue(4) -> [4]
enqueue(8) -> [4, 8]
dequeue()  -> removes 4; queue [8]
enqueue(9) -> [8, 9]
```

The front is `8`.

## Q8. Answer: C

A new node can be linked before the current head with a constant number of pointer assignments. Searching, accessing a position and finding the tail require traversal when only a head pointer is maintained.

## Q9. Answer: B

Inorder visits left subtree, node, then right subtree. The BST ordering property therefore produces keys in non-decreasing order.

## Q10. Answer: C

Sorted insertion order creates a chain: `10 -> 20 -> 30 -> 40` along right-child links. Its height is `n-1` edges, so searching can examine all `n` nodes: `O(n)`.

## Q11. Answer: B

In a max-heap, every parent is greater than or equal to its children. Following this property from the root to any node shows that the root is a maximum key.

## Q12. Answer: B

An adjacency matrix stores one cell for every ordered pair of vertices, giving `V x V = O(V^2)` space.

## Q13. Answers: A, B and D

- A is correct: every recursive path must eventually terminate.
- B is correct: active recursive calls commonly occupy call-stack frames.
- C is false: recursive algorithms can be constant, logarithmic, linear, polynomial or exponential, depending on their recurrence.
- D is correct: the maximum number of active calls determines call-stack depth.

## Q14. Answers: A, C and D

- A is correct: array element addresses are calculated directly.
- B is false: a linked list must be traversed node by node to reach a position.
- C is correct: head insertion requires a constant number of pointer operations.
- D is correct: elements normally shift right to make room at the beginning.

## Q15. Answers: A, C and D

- A is correct: a perfect tree fills every level, including the last, and is therefore complete.
- B is false: a complete tree may have a partially filled last level.
- C is the definition of a full/proper binary tree.
- D is the definition of a binary tree.

## Q16. Answers: A, B and D

- A is correct by the max-heap property.
- B is correct because a binary heap is complete.
- C is false: a heap does not impose the full ordering rule of a BST.
- D is correct because insertion may move a node up at most the heap height, `O(log n)`.

## Q17. Answers: A, B and C

- A is correct: standard BFS uses a queue.
- B is correct: recursive DFS uses the call stack.
- C is correct: BFS explores vertices in non-decreasing distance (edge count) from the source.
- D is false: one source reaches only its reachable component. A loop over unvisited vertices is needed to cover a disconnected graph.

## Q18. Answer: 1236

Use:

\[
\operatorname{LOC}(A[9])=1200+9\times4=1236
\]

## Q19. Answer: 1026

There are 5 columns. In row-major order:

\[
\operatorname{LOC}(A[2][3])=1000+((2\times5)+3)\times2
\]

\[
=1000+(13\times2)=1026
\]

**Correct answer: 1026.** The offset is 13 elements, or 26 bytes.

## Q20. Answer: 31

For a perfect binary tree of height `h` measured in edges:

\[
N=2^{h+1}-1=2^{5}-1=31
\]

## Q21. Answer: 13

For a full binary tree, leaves `n0 = n2 + 1`. With 12 nodes having two children:

\[
n_0=12+1=13
\]

## Q22. Answer: 7

\[
(rear+1)\bmod 8=(6+1)\bmod8=7
\]

## Q23. Answer: 15

For a zero-indexed heap, left child index is `2i + 1`:

\[
2(7)+1=15
\]

## Q24. Answer: 14

For an undirected graph, the sum of all vertex degrees equals twice the number of edges:

\[
\sum\deg(v)=2|E|=2\times7=14
\]

## Q25. Answer: `15`

`p` stores the address of `x`. The expression `*p = *p + 5` reads `x` through the pointer, adds 5, and writes the result back to `x`. Therefore `x` becomes 15.

## Q26. Answer: `10`

Expansion:

```text
sum(4) = 4 + sum(3)
       = 4 + 3 + sum(2)
       = 4 + 3 + 2 + sum(1)
       = 4 + 3 + 2 + 1 + sum(0)
       = 4 + 3 + 2 + 1 + 0
       = 10
```

## Q27. Answer: `4`; stack from bottom to top: `[2, 4]`

Trace:

```text
push(2) -> [2]
push(4) -> [2, 4]
push(6) -> [2, 4, 6]
pop()   -> removes 6; [2, 4]
push(8) -> [2, 4, 8]
pop()   -> removes 8; [2, 4]
peek()  -> returns 4; stack remains [2, 4]
```


## Q28. Three-pointer reversal

Maintain `prev = NULL`, `current = head`, and on every iteration save `next = current->next`. Change `current->next = prev`, then move `prev = current` and `current = next`. At the end, return `prev` as the new head.

- Time: `O(n)`, because each node is processed once.
- Auxiliary space: `O(1)`, because only a constant number of pointers are used.

## Q29. BST answer

Insertion produces:

```text
          40
        /    \
       20     60
      / \    / \
     10 30  50 70
```

Inorder traversal: `10, 20, 30, 40, 50, 60, 70`.

The root's inorder successor is `50`, the minimum key in the root's right subtree.

## Q30. Max-heap deletion

Initial heap:

```text
[50, 30, 40, 10, 20, 35]
```

1. Remove maximum `50`.
2. Move the last value `35` to the root and reduce the heap size:

```text
[35, 30, 40, 10, 20]
```

3. Compare root 35 with children 30 and 40. The larger child is 40, so swap:

```text
[40, 30, 35, 10, 20]
```

The heap property now holds. **Result:** `[40, 30, 35, 10, 20]`.

## Q31. BFS answer

Adjacency order is given, and vertices are marked visited when enqueued.

```text
Start: enqueue A; queue [A]
Remove A; visit A; enqueue B, C; queue [B, C]
Remove B; visit B; enqueue D, E; queue [C, D, E]
Remove C; visit C; A is visited, enqueue F; queue [D, E, F]
Remove D; visit D; B is visited; queue [E, F]
Remove E; visit E; B and F are visited; queue [F]
Remove F; visit F; C and E are visited; queue []
```

BFS order: `A, B, C, D, E, F`.

## Q32. Complexity comparison

A **max-heap** is usually the best fit when the two frequent operations are insertion and retrieval/removal of the current largest item:

- Inspect maximum: `O(1)`.
- Insert: `O(log n)`.
- Remove maximum: `O(log n)`.

An unsorted array can insert at the end in `O(1)` when capacity is available, but finding the largest item takes `O(n)`. An ordinary BST has `O(h)` insertion and maximum lookup; it may become skewed, making these operations `O(n)`. A self-balancing BST can provide logarithmic updates and ordered operations, but that is a different, more specialized structure.

---

# 16. Quick revision sheet

## 16.1 C essentials

- C uses pass-by-value. Passing a pointer copies the address value.
- `&x` gives an address; `*p` dereferences a pointer.
- `a[i]` is equivalent to `*(a+i)` for a valid array element.
- Pointer arithmetic is scaled by the pointed-to type.
- C multidimensional arrays are row-major.
- A C string ends with `\0`.
- `malloc` allocates uninitialized bytes; `calloc` initializes allocated bytes to zero; `realloc` resizes; `free` releases.
- Check bounds and pointer validity; C does not automatically protect every memory access.

## 16.2 Recursion essentials

- Every recursive solution needs a base case and progress toward it.
- Active calls use call-stack space.
- `T(n)=T(n-1)+O(1)` gives `O(n)` time.
- `T(n)=T(n/2)+O(1)` gives `O(log n)` time.
- Naive Fibonacci is exponential in time and `O(n)` in maximum call depth.
- Recursive binary search is `O(log n)` time and `O(log n)` stack space.

## 16.3 Array formulas

One-dimensional address:

\[
B+(i-LB)w
\]

Two-dimensional row-major address:

\[
B+((i-LR)C+(j-LC))w
\]

Two-dimensional column-major address:

\[
B+((j-LC)R+(i-LR))w
\]

## 16.4 Stack and queue

- Stack = LIFO; push/pop at top.
- Queue = FIFO; enqueue at rear, dequeue at front.
- Array stack initially uses `top = -1`.
- Circular queue (front/rear sentinel convention): empty if `front == -1`; full if `(rear+1)%N == front`.
- Standard stack and queue end operations are `O(1)`.

## 16.5 Linked lists

- Singly list node: data + next pointer.
- Doubly list node: data + prev + next.
- Circular list links the final node back to the first.
- Head insertion/deletion: `O(1)`.
- Search and random position access: `O(n)`.
- Iterative reversal: `O(n)` time, `O(1)` auxiliary space.
- Floyd cycle detection: `O(n)` time, `O(1)` auxiliary space.

## 16.6 Trees and BSTs

- A tree with `n` nodes has `n-1` edges.
- Binary tree: at most two children per node.
- Maximum nodes at level `l`: `2^l`.
- Maximum nodes at height `h` edges: `2^(h+1)-1`.
- Full binary tree: each node has 0 or 2 children; leaves = two-child nodes + 1.
- Traversals: preorder NLR, inorder LNR, postorder LRN, level-order uses a queue.
- BST inorder traversal is sorted.
- BST search/insert/delete: `O(h)`; balanced `O(log n)`, skewed `O(n)`.

## 16.7 Binary heaps

For zero-based indexing:

- Parent: `floor((i-1)/2)` for `i > 0`.
- Left child: `2i+1`.
- Right child: `2i+2`.

For one-based indexing:

- Parent: `floor(i/2)`.
- Left child: `2i`.
- Right child: `2i+1`.

- Max-heap root is maximum; min-heap root is minimum.
- Insert and delete root: `O(log n)`.
- Peek root: `O(1)`.
- Bottom-up build-heap: `O(n)`.
- Search arbitrary key: `O(n)`.
- Heap sort: `O(n log n)` time, `O(1)` auxiliary space in the standard in-place form.

## 16.8 Graphs

- Graph: `G=(V,E)`.
- Undirected degree sum: `2E`.
- Directed indegree sum = directed outdegree sum = `E`.
- Adjacency matrix: `O(V^2)` space; edge lookup `O(1)`.
- Adjacency list: `O(V+E)` space.
- BFS uses a queue; DFS uses a stack or recursion.
- BFS finds shortest paths by edge count in an unweighted graph.
- BFS/DFS with adjacency lists: `O(V+E)`.
- A disconnected graph needs a new traversal from each unvisited vertex to cover all components.
- A topological ordering exists exactly for a DAG.

---

## Final self-check

Before considering this topic complete, make sure you can:

- Trace C expressions involving arrays, pointers, functions and recursion.
- Write and analyze iterative and recursive algorithms.
- Calculate one- and two-dimensional array addresses.
- Implement stack and queue operations and identify overflow/underflow conditions.
- Explain why a circular queue avoids the simple linear queue's wasted-front-space problem.
- Insert, delete, traverse and reverse linked lists safely.
- Identify tree types, calculate tree properties and produce traversal sequences.
- Perform BST search, insertion and all three deletion cases.
- Insert into a heap, delete its root, build a heap and explain heap sort.
- Choose a graph representation and trace BFS/DFS with the correct visited order.
- State time and auxiliary-space complexity, including worst-case conditions.

**End of study material.**
