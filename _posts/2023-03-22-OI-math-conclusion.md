---
layout: post
title: OI数学专题总结
author: EM
date: 2023-03-22
categories: OI
tags: [笔记]

---



对过去几周的数学学习做一些总结……

## 数论

### 专题1

#### 唯一分解定理

唯一分解定理，又名算术基本定理。

$$n=p_1^{r_1}p_2^{r_2}\cdots p_k^{r_k}=\prod\limits_{i=1}^{k}p_i^{r_i}$$

where $$n\in Z,n>1,p$$为质数

##### 推导：欧拉函数

$$\varphi(n)=n(1-\dfrac{1}{p_1})(1-\dfrac{1}{p_2})\cdots(1-\dfrac{1}{p_3})$$

- 利用容斥推导

##### 推导：约数个数函数

$$d(n)=(r_1+1)(r_2+1)\cdots(r_k+1)$$

##### 推导：约数和函数

$$\sigma(n)=(1+p_1+p_1^{2}+\cdots+p_1^{r_1})\cdots(1+p_k+p_k^{2}+\cdots+p_k^{r_k})$$

#### 质因数分解

##### 算法1

试除$$[2,\sqrt{n}]$$内的整数

时间复杂度$$O(\sqrt{n})$$

##### 算法2

- $$O(\sqrt{n})$$处理$$[2,\sqrt{n}]$$内的质数
- 分解时仅试除质数

时间复杂度$$\dfrac{O(\sqrt{n})}{O(\dfrac{\sqrt{n}}{\log_{2}{n}})}$$

##### 算法3

- 欧拉筛时记录每个数的最小质因数
- 分解时直接除去最小质因数

时间复杂度$$\dfrac{O(n)}{O(\log_{2}n)}$$

#### 找约数

##### 算法1

试除$$[1,\sqrt{n}]$$内的整数

时间复杂度$$O(\sqrt{n})$$

##### 算法2

- 利用未优化埃筛思想，预处理$$[1,n]$$里每个数的约数

参考代码：

```c++
for (int i = 1; i <= n; i++) for (int j = i; j <= n; j += i) f[j].push_back(i);
```

时间复杂度$$O(n\log_{2}n)$$

##### 算法3

- 分解质因数
- dfs或循环枚举质因数指数

### 专题2

#### 欧拉函数

各种等式们：

$$Z_{n}^*$$中所有元素和为$$\dfrac{n\varphi(n)}{2}$$

$$\varphi(i)=\sum\limits_{i=1}^{k}\varphi(p_i^{r_i})$$，where $$\varphi(p^k)=p^k-p^{k-1}$$

$$n=\sum\limits_{d|n}\varphi(d)$$

#### 乘法取模

##### 实现1

龟速乘，dddd

复杂度$$O(log_2n)$$

##### 实现2

神必的做法

```c++
#define int long long  // 坏习惯，益终生
int qqt(int x, int y, int m) {
    int ret = x * y - (int)((long double) x * y / m + 1e-8) * m;
    return ret < 0 ? ret + m : ret;
}
```

#### 欧拉降幂公式

当$$b\geq \varphi(m)$$

$$a^b\equiv a^{b\mod\varphi(m)+ \varphi(m)}\pmod m$$
