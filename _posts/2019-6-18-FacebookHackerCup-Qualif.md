---
layout: post
title: Facebook hacker cup 2019 - Qualification Round
---

This article shows you how I solved the first three problems of the qualification round of Facebook Hacker Cup 2019.

Here are the problems: [Facebook hacker Cup]().

**Leapfrog: Ch. 1**:

For this problem, given a string of `A`, `B` and `.` we had to determine if it was possible for `A` which was at index 1 to reach the rightmost cell.
Constraints: `A` can move **only** to its right and it can jump over `B` ,`B` can move to both directions.

For example, if we have `A.B.B` it is possible for `A` to reach the rightmost cell in four steps :
1- `AB..B`
2- `AB.B.`
3- `.BAB.`
4- `.B.BA`

The solution is pretty clear : count the occurrence of `B` and `.`, if `B` occurrence is equal or higher than the occurrence of `.` and there is at least one `.`, the answer is "Y" otherwise it's "N".

```cpp
#include <iostream>
#include <bits/stdc++.h>
#include <vector>
#include <stdio.h>
using namespace std;

int main()
{
	ios::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0);
	int test;
	cin >> test;
	for (int t = 0; t < test; t++)
	{
		string arr;
		cin >> arr;
		int countB = count(arr.begin(), arr.end(), 'B');
		int countPoint = count(arr.begin(), arr.end(), '.');

		if (countB >= countPoint && countPoint > 0)
		{
			cout << "Case #" << t + 1 << ": Y"
				 << "\n";
		}
		else
		{
			cout << "Case #" << t + 1 << ": N"
				 << "\n";
		}
	}
}
```

**Leapfrog: Ch. 2**:

For this problem, the solution is similar to the first one, but we have another constraint : `A` can move in both directions.

It means that we can have this pattern with only 2 `B`:
1- `ABB...`
2- `AB.B..`
3- `.B.BA.`
4- `..BBA.`
4- `.ABB..`
4- `.AB.B.`
4- `..B.BA`

Then we can have `Y` answer if there is more than one `B`.
Just take the previous answer and add this new condition.

```cpp
#include <iostream>
#include <bits/stdc++.h>
#include <vector>
#include <stdio.h>
using namespace std;

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    int test;
    cin >> test;
    for (int t = 0; t < test; t++)
    {
        string arr;
        cin >> arr;
        int countB = count(arr.begin(), arr.end(), 'B');
        int countPoint = count(arr.begin(), arr.end(), '.');

        if ((countB >= countPoint || countB >= 2) && countPoint > 0)
        {
            cout << "Case #" << t + 1 << ": Y"
                 << "\n";
        }
        else
        {
            cout << "Case #" << t + 1 << ": N"
                 << "\n";
        }
    }
}
```

**Mr. X**:

This problem was pretty easy to solve with an interpreted language.
In fact, if the evaluation of the boolean expression with `x=true` is equal to that with `x=false`, it means that we have nothing to change: the answer is 0.
Otherwise the answer is 1 : there is at least one operator which leads to a constant value :

```
- If one of them is “0” then “&” can be used
- Otherwise, if one of them is “1”, then “|” can be used
- Otherwise, both are variable values, and “^” can be used
```

(from [Facebook Hacker Cup Solutions](https://www.facebook.com/notes/facebook-hacker-cup/hacker-cup-2019-qualification-round-solutions/2797355073613709/))

```py
test_cases = int(input())

for test_ in range(1, test_cases + 1):
    strings = str(input())

    true_value = eval(strings.replace('&', ' and ').replace('|', ' or ').replace('X', ' 0 ').replace('x', ' 1 '))
    false_value = eval(strings.replace('&', ' and ').replace('|', ' or ').replace('x', ' 0 ').replace('X', ' 1 '))

    if true_value == false_value:
        print('Case #{}: {}'.format(test_, "0"))
    else:
        print('Case #{}: {}'.format(test_, "1"))
```
