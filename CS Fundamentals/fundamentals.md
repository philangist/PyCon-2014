Big O Notation -  approximation of algorithmic complexity
---

Types of Big O
O(1, log n, n, n^2, n!),

O(1)

Get an element from an array

```python

def get_from_list(idx, lst):
    return lst[idx]

```


O(n)

For loops are the canonical example of O(n)

```python
    def item_in_list(item, lt):
        for entry in item: O(n)
            if item == lst # constant tim O(1)
                return True O(1)
        return False
```

We ignore lower polynomials in the big O complexity equation for a function

Example:
    Big O: O(n) * O(1) + O(1)

    O(n) always = x (linear function)

    x * 5 + 9

    if we graph ^ that function, we see that after a constant K (which is three), it will never cross the O(x) line

    It's technically O(n^2) as well, but that's not the "best" approximation of it's algorithmic complexity

N.B: item_in_list is actually constant if the input is empty, but with Big-O notation, were looking for worst time performance


O(log n)

Each iteration is a fraction of the search space

Binary Search on a sorted list


O (n^2)

For loops are O(n)
Nest for loops are O(n^2)

```python
def inner loop(matrix):
    for row in matrix:      O(n)
        for column in row:  O(n)
            a = column * 2  O(1)
            print a         O(1)

```

O(n) * (O(n)  + O(1) + O(1))


Gotchas:
The big O of a function might not matter (for small sample sizes)
Theoretical speed is different from the practical speed of a function
This stuff is probably not going to make your app faster because
performace bottlenecks are typically IO bound, not CPU bound.


Resource:
Algorithm Design Manual
Stanford Coursera Course - Algorithms Design and Analysis

Computer Science for Self Taught Programmers
