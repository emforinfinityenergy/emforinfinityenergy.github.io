---
layout: post
title: OI数学专题总结
author: EM
date: 2023-03-22
categories: OI
description: 对过去几周的数学学习做一些总结……
tags: [笔记]

---

## 数论

### 专题1

#### 唯一分解定理

唯一分解定理，又名算术基本定理。

$$n=p_1^{r_1}p_2^{r_2}\cdots p_k^{r_k}=\prod\limits_{i=1}^{k}p_i^{r_i}$$，where $$n\in Z,n>1,p$$为质数

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

$$n=\sum\limits_{d|n}\varphi(d)$$，where $$n\geq2$$

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

#### 除法取模

 $$\dfrac{a}{b} \bmod p = \dfrac{a\bmod bp}{p}$$

#### 欧拉降幂公式

当$$b\geq \varphi(m)$$

有$$a^b\equiv a^{b\mod\varphi(m)+ \varphi(m)}\pmod m$$

### 专题3

#### 二元一次不定方程

二元一次方程是指形如$$ax+by=c$$的方程。

接下来，我们将探寻这个方程的解。

##### 基本推导

易得，$$\gcd(a,b) \mid ax+by$$

$$\therefore$$该方程有解的必要条件为$$\gcd(a,b) \mid c$$

##### 裴蜀定理

方程$$ax+by=\gcd(a,b)$$必有整数解

利用裴蜀定理，我们可以将上述必要条件转化为充要条件。

设$$d=\gcd(a,b)$$

我们假设有另一个方程$$ax+by=d$$，$$\begin{align} \left\{ \begin{array} \newline x=x_0 \newline y=y_0  \end{array}\right .\end{align}$$ 为其一组解，则可以推导出$$\begin{align} \left\{ \begin{array} \newline x=\dfrac{c}{d} \times x_0 \newline y=\dfrac{c}{d} \times y_0  \end{array}\right .\end{align}$$ 为方程$$ax+by=c$$的一组解

##### 扩展欧几里得算法

扩展欧几里得算法是一种基于欧几里得算法（即辗转相除法）的算法，该算法可以帮我们求出$$ax+by=\gcd(a,b)$$的一组解。

模板代码如下：

```c++
#define int long long
int exgcd(int a, int b, int& x, int& y) {
	if (b == 0) {
		x = 1;
		y = 0;
		return a;
	}
	int p = exgcd(b, a % b, y, x);
	y -= a / b * x;
	return p;
}
```



 求出方程$$ax+by=\gcd(a,b)=d$$的一组解后，我们便可以得到原方程$$ax+by=c$$的所有解，方法如下：

1. 求出$$ax+by=d$$的一组解$$\begin{align} \left\{ \begin{array} \newline x=x_0 \newline y=y_0  \end{array}\right .\end{align}$$
2. 得到方程$$ax+by=c$$的一组解$$\begin{align} \left\{ \begin{array} \newline x_1=x_0 \times \dfrac{c}{d} \newline y_1=y_0 \times \dfrac{c}{d}  \end{array}\right .\end{align}$$
3. 根据上述解推出原方程所有解$$\begin{align} \left\{ \begin{array} \newline x=x_1 + \dfrac{b}{d} \times k \newline y=y_1 - \dfrac{a}{d} \times k  \end{array}\right .\end{align}$$，where$$k\in Z$$

##### 多元一次不定方程的求解

尝试解$$a_1x_1+a_2x_2+\cdots+a_nx_n=b$$，方法如下：

我们先解$$a_1x_1+a_2x_2=\gcd(a_1,a_2)=g_2$$

然后我们将$$a_1x_1+a_2x_2$$代换为$$g_2t_2$$

原方程化为$$g_2t_2+a_3x_3+\cdots+a_nx_n=b$$

重复上述步骤，直到原方程剩下$$g_{n-1}t_{n-1}+a_nx_n=b$$

反复扩欧解上述方程，解出所有$$x$$。

由上述解法和裴蜀定理可看出，原方程有解的充要条件为$$\gcd(a_1,a_2,\cdots,a_n) \mid b$$

#### 线性同余方程与中国剩余定理

##### 线性同余方程

形如$$ax\equiv b\pmod{m}$$的方程

##### 中国剩余定理

中国剩余定理是求解线性同余方程组的一种算法。

求解的方程组应满足形式$$\begin{align} \left\{ \begin{array} \newline x \equiv a_1 \pmod{r_1} \newline x \equiv a_2 \pmod{r_2} \newline\vdots\newline x \equiv a_k \pmod{r_k}  \end{array}\right .\end{align}$$

模板如下：

```c++
#define int long long
int a[1005], r[1005];

int qt(int x, int y, int mod) {
    int ret = x * y - (int)((long double)x * y / mod + 1e-8) * mod;
    return ret < 0 ? ret + mod : ret;
}

int exgcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int p = exgcd(b, a % b, y, x);
    y -= a / b * x;
    return p;
}

int CRT(int k) {
    int n = 1, ans = 0;
    for (int i = 1; i <= k; i++) n = n * r[i];
    for (int i = 1; i <= k; i++) {
        int m = n / r[i], b, y;
        exgcd(m, r[i], b, y);
        ans = (ans + qt(qt(a[i], m, n), b, n)) % n;
    }
    return (ans % n + n) % n;
}
```
