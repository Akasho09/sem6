## 
1. Step 1: Split the numbers
Let x = 1234, y = 4321.
We split each into two halves:
- x = 1234 = 12*100 + 34 = x1*B + x0 where x1 = 12, x0 = 34
- y = 4321 = 43*100 + 21 = y1*B + y0 where y1 = 43, y0 = 21

> B = 100 (base = 10^2 since we split into 2-digit halves)

2. Step 2: Apply Karatsuba Formula
Karatsuba’s algorithm:
    xy = z2 * B^2 + (z1 - z2 - z0) * B + z0
    where:
    z2 = x1 * y1
    z0 = x0 * y0
    z1 = (x1 + x0)(y1 + y0)

Compute:
z2 = 12 × 43 = 516
z0 = 34 × 21 = 714
(x1 + x0) = 46, (y1 + y0) = 64
z1 = 46 × 64 = 2944
Now compute:
middle = z1 - z2 - z0 = 2944 - 516 - 714 = 1714
Now compute the final result:
xy = z2 * 100^2 + middle * 100 + z0 = 516 * 10000 + 1714 * 100 + 714
xy = 5160000 + 171400 + 714 = 5332114
✅ Answer: 1234 × 4321 = 5332114

## Egg Dropping Problem
Optimal Strategy:
Use the mathematical approach:

We choose floors in decreasing steps:
Try floor x, then x-1, x-2, ..., until 100.

So the sum must satisfy:
x + (x - 1) + (x - 2) + ... + 1 ≥ 100
=> x(x + 1)/2 ≥ 100
Solving:

x(x + 1) ≥ 200
Try x = 14 → 14*15 = 210 ✅
Strategy:
Drop 1st egg from 14th floor
Then from (14 + 13) = 27
Then (27 + 12) = 39
Continue until it breaks.

When it breaks, do linear search with 2nd egg from the previous floor +1.
✅ Minimum worst-case drops = 14
✅ Time Complexity: O(√n) for 2 eggs and n floors.

## BUILD-MAX-HEAP on array
heapify at diff poistions.