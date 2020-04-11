---
layout: post
title: Google Code Jam 2020 - Qualification round
---

This article contains my solutions for the Google Code Jam 2020 Qualification round.
The code was not touched and remain as I submitted it.  
**Rank**: **7126** / 40698

| **Problems**                 | **Test Cases** |
| ---------------------------- | :------------: |
| Vestigium                    |       ✅       |
| Nesting Depth                |      ✅✅      |
| Parenting Partnering Returns |      ✅✅      |
| ESAb ATAd                    | Not attempted  |
| Indicium                     |      ✅❌      |

**Vestigium**

```py
from sys import stdin

test_cases = int(stdin.readline())

for test in range(1, test_cases + 1):
    n = int(stdin.readline())
    arr = []
    for i in range(n):
        arr.append(list(map(int, stdin.readline().split())))

    diag = 0
    r = 0
    c = 0

    rows = [[] for i in range(n)]
    col = [[] for i in range(n)]

    #
    for i in range(n):
        for y in range(n):
            if i == y:
                diag += arr[i][y]
            rows[i].append(arr[i][y])
            col[y].append(arr[i][y])

    for i in range(n):
        for el in rows[i]:
            if rows[i].count(el) > 1:
                r += 1
                break

    for i in range(n):
        for el in col[i]:
            if col[i].count(el) > 1:
                c += 1
                break

    result = str(diag) + " " + str(r) + " " + str(c)
    print('Case #{}: {}'.format(test, str(result)))
```

**Nesting Depth**

```py
from sys import stdin

test_cases = int(stdin.readline())

def solve(arr):
    depth = arr[0]
    result = "("*depth + str(arr[0])
    for i in range(1, len(arr)):
        if arr[i] == depth:
            result += str(arr[i])
            continue
        elif arr[i] > depth:
            diff = abs(depth - arr[i])
            depth = arr[i]
            result += "("*diff
            result += str(arr[i])
        else:
            diff = abs(depth - arr[i])
            depth = arr[i]
            result += ")"* diff
            result += str(arr[i])

    result += ")"*depth

    return result


for test in range(1, test_cases + 1):
    arr = stdin.readline().strip()

    rr = arr.split("0")

    for i in range(len(rr)):
        if len(rr[i]) > 0:
            rr[i] = solve([int(el) for el in rr[i]])

    result = "0".join(rr)

    print('Case #{}: {}'.format(test, str(result)))
```

**Parenting Partnering Returns**

```py
from sys import stdin

test_cases = int(stdin.readline())

def range_overlapping(x, y):
    if x.start == x.stop or y.start == y.stop:
        return False
    return ((x.start < y.stop  and x.stop > y.start) or
            (x.stop  > y.start and y.stop > x.start))

def check(range1, range2):
    t1 = range(range1['fromm'], range1['to'])
    t2 = range(range2['fromm'], range2['to'])

    return range_overlapping(t1, t2)

for test in range(1, test_cases + 1):
    n = int(stdin.readline())
    arr = []
    for i in range(1, n+1):
        fromm, too = list(map(int, stdin.readline().split()))
        arr.append({'fromm': fromm, 'to': too, 'index': i})

    arr = sorted(arr, key=lambda el: el['fromm'], reverse=False)

    first = None
    second = None

    ok = True

    result = ["" for i in range(n)]

    for i in range(n):
        if not first:
            result[arr[i]['index'] - 1] = "C"
            first = arr[i]
            continue
        if not second:
            result[arr[i]['index'] - 1] = "J"
            second = arr[i]
            continue

        if not check(first, arr[i]):
            first['to'] = max(arr[i]['to'], first['to'])
            first['fromm'] = min(arr[i]['fromm'], first['fromm'])
            result[arr[i]['index'] - 1] = "C"
        elif not check(second, arr[i]):
            second['to'] = max(arr[i]['to'], second['to'])
            second['fromm'] = min(arr[i]['fromm'], second['fromm'])
            result[arr[i]['index'] - 1] = "J"
        else:
            ok = False
            break

    if ok:
        print('Case #{}: {}'.format(test, "".join(result)))
    else:
        print('Case #{}: {}'.format(test, "IMPOSSIBLE"))
```

**Indicium**

```py
from sys import stdin

def sums(n_perm_elements, sum_total, min_value, max_value):
    if n_perm_elements == 1:
        if (sum_total <= max_value) & (sum_total >= min_value):
            yield (sum_total,)
    else:
        for value in range(min_value, max_value + 1):
            for permutation in sums(
                n_perm_elements - 1, sum_total - value, min_value, max_value
            ):
                yield (value,) + permutation

def find_empty_location(arr,l):
    for row in range(len(arr)):
        for col in range(len(arr)):
            if(arr[row][col]==0):
                l[0]=row
                l[1]=col
                return True
    return False

def used_in_row(arr,row,num):
    for i in range(len(arr)):
        if(arr[row][i] == num):
            return True
    return False

def used_in_col(arr,col,num):
    for i in range(len(arr)):
        if(arr[i][col] == num):
            return True
    return False


def check(arr, row, col, num):
    return not used_in_row(arr,row,num) and not used_in_col(arr,col,num)

def solve(arr, k):

    l=[0,0]

    if not find_empty_location(arr,l):
        return True

    row = l[0]
    col = l[1]

    for num in range(1, k+1):
        if check(arr,row,col,num):

            arr[row][col]=num

            if solve(arr, k):
                return True

            arr[row][col] = 0
    return False

def cc(arr, k):
    ok = True
    # Check row elements from 1 to k
    for el in arr:
        tt = sorted(el)
        if tt[0] != 1 or tt[-1] != k:
            ok = False
            break
    # Check column elements from 1 to k
    for i in range(len(arr)):
        tt = []
        for y in range(len(arr)):
            tt.append(arr[y][i])
        tt = sorted(tt)
        if tt[0] != 1 or tt[-1] != k:
            ok = False
            break
    return ok



if __name__=="__main__":
    test_cases = int(stdin.readline())

    for test in range(1, test_cases + 1):
        n, k = list(map(int, stdin.readline().split()))
        ok = False
        # 1 -  Test diagonal configuration with sum k
        for perm in sums(n, k, 1, n):
        # 2 - For each configuration check if it can leads to a solution
            arr = [[0 for i in range(n)] for y in range(n)]

            for i in range(n):
                for y in range(n):
                    if i == y:
                        arr[i][y] = perm[i]

            result = solve(arr, n)

            if result and cc(arr, n):
                ok = True
                print('Case #{}: {}'.format(test, "POSSIBLE"))
                for el in arr:
                    print(" ".join(list(map(str, el))))
                break

        if not ok:
            print('Case #{}: {}'.format(test, "IMPOSSIBLE"))
```
