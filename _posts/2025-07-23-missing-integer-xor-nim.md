---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Doc] Finding a Missing Integer in an Array Using XOR (Nim)"
date: 2025-07-23 03:51:09
categories: [Blog, Posts]
tags: [nim, xor, algorithm, array, bitwise, programming]
description: "A quick and elegant trick to find the missing integer in a sequence using XOR in Nim."
---

If you're dealing with a list of unique integers from 0 to _n_, and one is missing, there's a surprisingly efficient trick to find it—with just a single pass and constant space.

This post demonstrates how I implemented it in Nim using XOR.

### Why XOR?

XOR has a few neat properties:

- `x xor x = 0`
- `x xor 0 = x`
- It's **commutative** and **associative**

If you XOR all the numbers from 0 to _n_ and then XOR all the elements in your array, everything cancels out except the missing number.

---

### Example Code (Nim)

```nim
# Using xor to find the missing item in an array
proc findMissingInteger(array: openArray[int]): int =
  result = 0
  for integer in array:
    result = result xor integer

  for integer in 0..(array.len + 1):
    result = result xor integer

let arr1 = [8, 2, 4, 5, 3, 7, 1] # Missing = 6
let arr2 = [1, 2, 3, 5]          # Missing = 4

echo findMissingInteger(arr1)
echo findMissingInteger(arr2)
```

---

### Output

```bash
6
4
```

---

### When to Use This

- When you're given an array of size `n` that should contain all values from `0` to `n`, with one missing.
- You want a time-efficient (`O(n)`) and space-efficient (`O(1)`) solution.
- You're not allowed to sort the array or use extra data structures.

---

Got your own Nim tricks or optimizations? Let me know—always keen to see how others are applying bitwise logic outside of textbook problems.
