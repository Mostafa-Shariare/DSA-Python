## 🎓 1. What Is Big O Notation?

> **Big O** gives an **upper bound** on the **growth rate** of an algorithm in terms of input size `n`.

Mathematically, if we say an algorithm has **O(f(n))** time complexity, it means:

$$
\text{Time}(n) \leq C \cdot f(n), \text{ for some constant } C \text{ and for all large } n \geq n_0
$$

This means the algorithm’s running time grows **at most** as fast as `f(n)` times some constant `C`.

### ❗️What It Ignores:

* Machine speed
* Programming language
* Low-level optimizations
* Constants and lower-order terms

---

## 🧠 2. Why We Use It

To compare which algorithms **scale better** with huge inputs.

Let’s say:

* Algo A takes `0.0001 * n^2`
* Algo B takes `1000 * n`

For small `n`, Algo B seems slower. But for very large `n`, Algo A becomes **much** worse due to the **quadratic growth**.

---

## 📈 3. Common Time Complexities

| Big O      | Name          | Example                | Graph Shape   |
| ---------- | ------------- | ---------------------- | ------------- |
| O(1)       | Constant time | Access element in list | Flat line     |
| O(log n)   | Logarithmic   | Binary search          | Fast at start |
| O(n)       | Linear        | Loop over list         | Diagonal line |
| O(n log n) | Linearithmic  | Merge Sort             | Grows fast    |
| O(n²)      | Quadratic     | Nested loops           | Curve upward  |
| O(2^n)     | Exponential   | Recursive Fibonacci    | Explodes      |

Let’s visualize how `O(log n)` is different from `O(n)`, `O(n²)`, etc. (we already showed the graph above ☝️)

---

## 🧮 4. How to Analyze Time Complexity — Step by Step

Let’s say you have this:

```python
def example(arr):
    total = 0                     # O(1)
    for i in arr:                 # O(n)
        for j in arr:             # O(n)
            total += i * j        # O(1)
    return total                  # O(1)
```

### Step-by-step:

1. `total = 0` → runs once → **O(1)**
2. Outer loop runs `n` times.
3. Inner loop runs `n` times **for each** outer loop → total `n × n = n²` iterations.
4. So:

   $$
   T(n) = O(1) + O(n^2) + O(1) = O(n^2)
   $$

We **drop constants** and **non-dominant terms**, so `O(1 + n² + 1)` becomes **O(n²)**.

---

## 🔍 Let’s Go Deeper Into the Math

Suppose we write:

```python
for i in range(n):
    print(i)
```

You might think: “That’s one operation per iteration, so the total is `n` operations.”

Let’s represent it:

$$
T(n) = \sum_{i=1}^{n} 1 = n
\Rightarrow \boxed{O(n)}
$$

Another example:

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

Each `i` loops `n` times, and each `j` also loops `n` times:

$$
T(n) = \sum_{i=1}^{n} \sum_{j=1}^{n} 1 = n \times n = n^2
\Rightarrow \boxed{O(n^2)}
$$

### Binary Search Example (Logarithmic Time)

```python
def binary_search(arr, x):
    low = 0
    high = len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == x:
            return mid
        elif arr[mid] < x:
            low = mid + 1
        else:
            high = mid - 1
```

Here, the range (`high - low`) is halved every time. So, how many times can you divide `n` by 2 before you reach 1?

That’s:

$$
\log_2 n \Rightarrow \boxed{O(\log n)}
$$

---

## 🧠 5. Important Rules for Calculating Big O

### Rule 1: Ignore Constants

```python
for i in range(n):
    print(i)
for j in range(n):
    print(j)
```

→ `O(n + n)` = **O(n)**

### Rule 2: Drop Non-Dominant Terms

```python
for i in range(n):
    for j in range(n):
        print(i, j)
for k in range(n):
    print(k)
```

→ `O(n² + n)` = **O(n²)**

### Rule 3: Nested Loops → Multiply

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

→ `O(n * n)` = **O(n²)**

### Rule 4: Sequential → Add

```python
for i in range(n): print(i)     # O(n)
for j in range(n): print(j)     # O(n)
```

→ `O(n + n)` = **O(n)**

---

## 📦 6. Space Complexity: Just Like Time!

Tracks **how much memory** your algorithm uses.

Example:

```python
def make_array(n):
    arr = [0] * n
    return arr
```

Uses O(n) memory for storing `n` integers.

But:

```python
def sum_array(arr):
    total = 0
    for x in arr:
        total += x
    return total
```

→ Uses only a few variables → **O(1) space**

---

## 🧪 Challenge for You

What’s the time complexity of this?

```python
def mystery(n):
    i = 1
    while i < n:
        i *= 2
        print(i)
```

👉 Think: How many times can `i` be doubled before reaching `n`?

$$
2^k = n \Rightarrow k = \log_2 n \Rightarrow \boxed{O(\log n)}
$$


