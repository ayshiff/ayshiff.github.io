---
layout: post
title: Facebook Hacker Cup 2020 - Qualification round
---

This article contains my solutions for the Facebook hacker cup 2020 Qualification round.   
The code was not touched and remain as I submitted it.  

**Rank**: **10 624** / 32 699

| **Problems**                 | **Test Cases** (given test case / official test case) |
| ---------------------------- | :------------: |
| Travel Restrictions                    |       Not submited in time (✅✅)       |
| Alchemy               |      ✅✅      |
| Timber               |      ❌❌     |
| Running on Fumes - Chapter 1 |      ✅❌     |
| Running on Fumes - Chapter 2                    | Not attempted  |

## [Problem A: Travel Restrictions](https://www.facebook.com/codingcompetitions/hacker-cup/2020/qualification-round/problems/A)

My idea is to compute direct paths between countries (A -> B) and then all undirect paths (A -> B -> C -> ...)

**Python 3 solution:**

```py
from sys import stdin

test_cases = int(stdin.readline())

def solve(arr, visited, currentIn, currentOut):
    for el in range(len(arr)):
        if el not in visited:
            if arr[currentOut][el] == "Y" and abs(currentOut - el) <= 1:
                arr[currentIn][el] = "Y"
                arr = solve(arr, visited + [el], currentIn , el)
    return arr


for test in range(test_cases):
    n = int(stdin.readline())

    input_str = stdin.readline()
    output_str = stdin.readline()

    result = [["N" for i in range(n)] for y in range(n)]

    # Compute direct paths A -> B
    for i in range(n):
        for y in range(n):
            if abs(i - y) <= 1:
                if (input_str[y] == "Y" and output_str[i] == "Y") or (i == y):
                    result[i][y] = "Y"
    
    # Compute all undirect paths A -> B -> C ...
    for i in range(n):
        for y in range(n):
            if result[i][y] == "Y":
                result = solve(result,[i, y],i,y)

    print('Case #{}:'.format(test+1))
    for el in result:
        print("".join(el))

```

## [Problem B: Alchemy](https://www.facebook.com/codingcompetitions/hacker-cup/2020/qualification-round/problems/B)

One of the first note that we can make is that the order of the shards isn't important.
We can count the number of "A" shards and the number of "B" shards.

Each time we fuse two shards, the count of "A" shards and the count of "B" shards decrease by 1, respectively: (`AAB, BAA, ABA` => `A` and `BBA, ABB, BAB` => `B`).
It means that for each operation that we make, the difference between the count of "A" and "B" shards remains the same.
As N is always odd, we only have to check that `| countOfA - countOfB | == 1`, which means that there is a remaining letter at the end and the answer is "Y".

**Python 3 solution:**

```py
from sys import stdin

test_cases = int(stdin.readline()) 

for test in range(test_cases):
    n = int(stdin.readline())
    stones = str(stdin.readline())

    a = stones.count('A')
    b = stones.count('B')

    if abs(a-b) == 1:
        print('Case #{}: {}'.format(test+1, "Y"))
    else:
        print('Case #{}: {}'.format(test+1, "N"))
```

## [Problem D1: Running on Fumes - Chapter 1](https://www.facebook.com/codingcompetitions/hacker-cup/2020/qualification-round/problems/D1)

**NOTE:** My solution only passed the given input test, it is not a valid solution.

My idea was to brute-force the problem by trying all the different possibilities that could lead to a solution.

The next step to improve my current solution is to use dynamic programming.

**Python 3 solution:**

```py
from sys import stdin

test_cases = int(stdin.readline())

def solve(arr, amount, index, gaz, mm):
    if index == len(arr) - 1:
        return amount

    isBlock = False

    if index != 0:
        gaz -= 1

    if gaz == 0:
        amount = solve(arr, amount + arr[index], + index + 1, mm, mm)
    else:
        amount = min(solve(
            arr, amount + arr[index], index + 1, mm, mm), solve(arr, amount, index + 1, gaz, mm))

    if amount != float('inf'):
        isBlock = True

    if isBlock:
        return amount
    else:
        return float('inf')


for test in range(test_cases):
    n, m = list(map(int, stdin.readline().split()))
    arr = []

    for i in range(n):
        tt = int(stdin.readline())
        arr.append(float('inf') if tt == 0 else tt)
    
    result = solve(arr, 0, 0, m, m)

    print('Case #{}: {}'.format(test+1, -1 if result == float('inf') else result))

```