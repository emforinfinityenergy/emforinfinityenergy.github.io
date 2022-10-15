---
layout: post
title: 一元二次方程的解法
author: EM
date: 2022-10-15
categories: 笔记
tags: [数学]
---

## 定义

一元二次方程是指形如$$ax^{2} + bx + c = 0(a \neq 0)$$的方程

## 解法

### 配方法

将二次项，一次项和常数项配为**完全平方**后求解。

例如：
$$
x^{2} + 2x = 5
x^{2} + 2x + 1 = 6
(x+1)^{2} = 6
|x+1| = \sqrt{6}
x = \pm\sqrt{6} - 1
$$

### 公式法

本篇笔记的**重点**

 我们规定对于任意形如$$ax^{2} + bx + c = 0(a \neq 0)$$的方程，$$\Delta = b^{2} - 4ac$$ 为其**“判别式”**。

判别式用于**判定方程的根（解）的个数**。具体地，$$\begin{align}\left \{ \begin{array} \newline \Delta>0时，方程有两个不相等的根\newline\Delta=0时，方程有两个相等的根\newline \Delta < 0 时，方程没有实数根 \end{array} \right.\end{align}$$

若方程有实数根，则方程的根可以通过如下公式计算。
$$
x=\frac{-b\pm\sqrt{\Delta}}{2a}
$$


例如：
$$
x^{2} + 2x = 5
x^{2} + 2x - 5 = 0
\Delta = 4+20=24
\because\Delta>0
\therefore 方程有两个实数根
\therefore x=\frac{-b\pm\sqrt{\Delta}}{2a}
\therefore x = \pm\sqrt{6} - 1
$$
在解**难以配方或带二次根式或无法因式分解的一元二次方程中，使用公式法是极其有效的**。