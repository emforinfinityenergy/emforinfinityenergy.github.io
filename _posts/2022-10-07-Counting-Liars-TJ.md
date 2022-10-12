---
layout: post
title: USACO 2022 US Open Contest, Bronze, Problem 2 & NKOJ P9793 Counting Liars 题解
author: EM
date: 2022-10-07 12:00:00
categories: OI
tags: [题解,离散化]
---
本题是**USACO 2022 US Open Contest, Bronze, Problem 2**，以及**NKOJ P9793**

## **题意描述**

奶牛 Bessie 躲在数轴上的某处。Farmer John 的 $$N$$ 头奶牛（$$1\leq N\leq1000$$）中的每头奶牛都有一条信息要分享：第 $$i$$ 头奶牛说 Bessie 躲在小于或等于 $$p_{i}$$ 的某个位置，或者说 Bessie 躲在大于或等于 $$p_{i}$$ 的某个位置（$$1 \leq p_{i} \leq 10^9$$）。

不幸的是，可能不存在躲藏位置与所有奶牛的回答均一致，这意味着并非所有奶牛都在说真话。计算在撒谎的奶牛的最小数量。



### 输入格式（从终端 / 标准输入读入）：

输入的第一行包含 $$N$$。

以下 $$N$$ 行每行包含字符 `L` 或 `G`，之后是一个整数 $$p_{i}$$。L 表示第 $$i$$ 头奶牛说 Bessie 的躲藏位置小于或等于 $$p_{i}$$，而 G 表示第 $$i$$ 头奶牛说 Bessie 的躲藏位置大于或等于 $$p_{i}$$。

## **分析1（10pts）**

不计算最小数量，依靠在线算法，根据前面的操作判断后面的操作的正确性，无法判断的默认正确。

太简单，就不放代码了

## **分析2（100pts）**

根据题意，我们只需要枚举Bessie所在的点，然后统计其左侧的L奶牛和右侧的R奶牛之和。然而直接枚举需要枚举 $$10^9$$ 次。但是观察题面可以发现，Bessie是可以在奶牛所说的位置上的，因此我们只需要对信息排序之后枚举这些奶牛所说的点即可。总共枚举 $$N$$ 次。

代码：（100pts）

```c++
#include<bits/stdc++.h>
using namespace std;

int ans = 0xccfccfc;

struct node {
	char op;
	int p;
}a[1005];

bool cmp(node x, node y) {
	return x.p < y.p;
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int n;
	cin >> n;
	for (int i = 1; i <= n; i++) {
		cin >> a[i].op >> a[i].p;
	}
	sort(a + 1, a + n + 1, cmp);
	for (int i = 1; i <= n; i++) {
		int tans = 0;
		for (int j = 1; j <= n; j++) {
			if (j < i && a[j].op == 'L' && a[j].p != a[i].p) tans++;
			if (j > i && a[j].op == 'G' && a[j].p != a[i].p) tans++;
		}
		ans = min(ans, tans);
	}
	cout << ans;
	return 0;
```



**Thanks for reading.**

**EOF**

