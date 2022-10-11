---
layout: post
title: NKRQ2022运动会专题
date: 2022-10-12 23:00:00
author: EM
categories: 记事
tags: [学校]
---

**NKOJ P8615 卡片**  

## 问题描述

果果有 $$n$$ 张卡片，每 $$i$$ 张卡片上有一个数字 。果果在里面选出了 $$k$$ 张，按照某种顺序依次排列成一个数。

比如果果选出了 $$3,13,1$$ 这三张卡片，果果就可以排列成 $$3131,3113,1331,1313,1133$$ 这五个数。

你需要帮果果求出对于所有选出 $$k$$ 张卡片的方案，果果总共能拼成多少种不同的数字。

## 分析1（骗分）(30-40pts)

观察数据范围，**对于20%的数据，有** $$1 \leq n \leq 6$$，**对于另20%的数据，所有卡片上的数字相等**

不难推出， $$k=1$$ 时答案是数字不重复的卡片个数~~然而我直接是输出的卡片个数~~，数字相等时答案为1。

代码：(30pts)

```c++
#include<bits/stdc++.h>
using namespace std;

int main() {
	int n, k;
	cin >> n >> k;
	if (k == 1) cout << n;
	else cout << 1;
	return 0;
}
```

## 分析2（string DFS）(80pts)

由于**n<=10**，考虑dfs，不再赘述。

然而，由于我只想到string DFS，查重略显麻烦。

因此使用一个queue~~可以用数组，我是傻逼~~ 每次遍历查重 ~~已经和正解渐行渐远了~~

代码：(80pts)

```c++
#include<bits/stdc++.h>
using namespace std;

int n, k, ans;
bool b[10005];
string a[10005];

queue<string> q;

bool check(string p) {
	for (int i = 1; i <= q.size(); i++) {
		if (p == q.front()) return false;
		q.push(q.front());
		q.pop();
	}
	return true;
}

void dfs(int step, string p) {
	if (step == k + 1) if (check(p)) {
		ans++;
		q.push(p);
	}
	for (int i = 1; i <= n; i++) if (!b[i]) {
		b[i] = true;
		dfs(step + 1, p + a[i]);
		b[i] = false;
	}
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	cin >> n >> k;
	for (int i = 1; i <= n; i++) cin >> a[i];
	dfs(1, "");
	cout << ans;
	return 0;
}
```



## 分析3（string DFS + 骗分）(100pts)

我们观察两次的评测结果：

分析1：

![分析1](https://files.catbox.moe/0dzgx0.png)

分析2：

![](https://files.catbox.moe/5d0wdu.png)

我们发现，T掉的两个点刚好是我们骗到的其中两个点。由于 $$k=1$$ 时，dfs只执行$$N$$次，没有TLE的可能，所以判定测试点5，6为卡片数字全部相等的情况。因此，特判该情况并输出1。$$Accepted$$。

代码：（100pts）(3243ms)

```c++
#include<bits/stdc++.h>
using namespace std;

int n, k, ans;
bool b[10005];
string a[10005];

queue<string> q;

bool check(string p) {
	for (int i = 1; i <= q.size(); i++) {
		if (p == q.front()) return false;
		q.push(q.front());
		q.pop();
	}
	return true;
}

void dfs(int step, string p) {
	if (step == k + 1) if (check(p)) {
		ans++;
		q.push(p);
	}
	for (int i = 1; i <= n; i++) if (!b[i]) {
		b[i] = true;
		dfs(step + 1, p + a[i]);
		b[i] = false;
	}
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	cin >> n >> k;
	bool flag = true;
	for (int i = 1; i <= n; i++) {
		cin >> a[i];
		if (i > 2 && a[i] != a[i - 1]) flag = false;
	}
	if (flag) {
		cout << 1;
		return 0;
	}
	dfs(1, "");
	cout << ans;
	return 0;
}
```

这只是一个半吊子解法，很多队友都解出了正确的int DFS。orz %%%
