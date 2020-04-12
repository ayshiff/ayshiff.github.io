---
layout: post
title: Google Code Jam 2020 - Round 1A
---

This article contains my solutions for the Google Code Jam 2020 round 1A.
The code was not touched and remain as I submitted it.  
**Rank**: **1575** / 9413

| **Problems**     | **Test Cases** |
| ---------------- | :------------: |
| Pattern Matching |     ✅✅✅     |
| Pascal Walk      |     ✅✅✅     |
| Square Dance     | Not attempted  |

**Pascal Walk**

```py
from sys import stdin

test_cases = int(stdin.readline())

arr = []

DIR = [(-1, 0), (-1, -1), (0, 1), (0, -1), (1, 1), (1, 0)]

def binomialCoeff(n, k) :
    res = 1
    if (k > n - k) :
        k = n - k
    for i in range(0 , k) :
        res = res * (n - i)
        res = res // (i + 1)
    return res

# Construct Pascal's triangle
for line in range(0, 100):
    tt = []
    for i in range(0, line + 1):
        tt.append(binomialCoeff(line, i))
    arr.append(tt)

for test in range(1, test_cases + 1):
    n = int(stdin.readline())

    # DFS
    stack = [([(1, 1)], 1, (0, 0))]
    visited = [(0, 0)]

    while stack:
        path, cnt, point = stack.pop()

        if cnt == n and len(path) < 500:
            print('Case #{}:'.format(test))
            for el in path:
                print(el[0], el[1])
            break

        for dx, dy in DIR:
            if 0 <= dx + point[0] < len(arr) and 0 <= dy + point[1] < len(arr[dx + point[0]]):
                if (dx + point[0], dy + point[1]) not in visited and cnt < n:
                    visited.append((dx + point[0], dy + point[1]))
                    stack.append((path + [(dx + point[0] + 1, dy + point[1] + 1)], cnt + arr[dx + point[0]][dy + point[1]], (dx + point[0], dy + point[1])))
```

**Pattern Matching**

```py
from sys import stdin

test_cases = int(stdin.readline())

for test in range(1, test_cases + 1):
    n = int(stdin.readline())
    ok = True
    arr = []

    for i in range(n):
        arr.append(stdin.readline().strip())

    constructed = ["" for i in range(2000)]

    resultMiddle = ""

    for el in arr:
        indLeft = len(el) - 1
        indLeft2 = 1999
        indRight = 0

        while el[indRight] != "*":
            if constructed[indRight] == "" or constructed[indRight] == el[indRight]:
                constructed[indRight] = el[indRight]
                indRight += 1
            else:
                ok = False
                break

        while el[indLeft] != "*":
            if constructed[indLeft2] == "" or constructed[indLeft2] == el[indLeft]:
                constructed[indLeft2] = el[indLeft]
                indLeft -= 1
                indLeft2 -= 1
            else:
                ok = False
                break

        for i in range(indRight, indLeft):
            if el[i] != "*":
                resultMiddle += el[i]

    if ok:
        ind = 0
        for i in range(len(constructed)):
            if constructed[i] == "":
                ind = i
                break
        result = "".join(constructed[0:ind]) + resultMiddle + "".join(constructed[ind+1:])

    else:
        result = "*"
    print('Case #{}: {}'.format(test, str(result)))
```
