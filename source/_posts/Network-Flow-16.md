---
title: Network Flow Theroy -16
date: 2019-5-20 17:15:11
tags: 
- Network Flow Theroy
categories:
- 笔记
mathjax: true
---

&emsp;&emsp;这一篇笔记中涉及了原书的第16章内容

<!-- more -->

# 1.简介Introduction
## 1.1网络路径问题
在一个网络$G=(N,A)$中，$N$表示节点的集合，$A$表示弧段的集合。其中，
## 1.2基本形式
Origin problem (P)
$$
  \min cx \\
  Ax \leqslant b \\
  Cx \leqslant d \\
  x = \left\{ {0,1} \right\}  
$$
-其中$Ax \leqslant b$是复杂约束，$Cx \leqslant d$是简单约束。
## 1.3例子
考虑一个带有路径长度约束的最短路问题，它具有如下形式
$$
\min \sum_{(i, j) \in A} c_{i j} x_{i j}\\
s.t.\sum_{\{j :(i, j) \in A \}} x_{i j}-\sum_{\{j :(j, i) \in A\}} x_{j i}=\left\{\begin{aligned} 1 & \text { for } i=1 \\ 0 & \text { for } i \in N \backslash \left\{1, n\right\} \\-1 & \text { for } i=n \end{aligned}\right. \\
\sum_{(i, j) \in A} t_{i j} x_{i j} \leq T\\
x_{i j}=0 \text { or } 1 \quad \text { for all }(i, j) \in A
$$

# 2.拉格朗日松弛技术(A LAGRANGIAN RELAXATION TECHNIQUE)
##2.1 拉格朗日乘子问题
对于原始问题(P)，构造拉格朗日松弛/子问题(Lagrangian relaxation / Lagrangian subproblem)
$$
\begin{gathered}
  {\text{Minimize }}cx + \mu (Ax - b) \hfill \\
  Cx \leqslant d \hfill \\
  x = \left\{ {0,1} \right\} \hfill \\ 
\end{gathered}
$$
**拉格朗日函数**(Lagrangian Function)定义为：
$$
L(\mu)=\min \{c x+\mu(Ax-b) : x \in X\}
$$
- $ X = \left\{ x|Cx \leqslant d,x = \left\{ {0,1} \right\} \right\}$， 并且我们假定集合$X$是有限的，所以$X=\{x^1,x^2,\cdots,x^K\}$。

**Lemma (Lagrangian Bounding Priciple)** For any vector $\mu​$ of the Lagrangian multipliers, the value L($\mu​$) of the Lagrangian function is a lower bound on the optimal objective function value $z^*​$ of the original optimization problem (P). 

这个定理表达为：
$$
z^{*} \geq \min \{c x+\mu(Ax-b) : x \in X\}=L(\mu)
$$
**拉格朗日乘子问题**(Lagrangian multiplier problem)
$$
L^{*}=\max _{\mu \geq 0} L(\mu)
$$
**弱对偶性**(Weak Duality) The optimal objective function value $L^*​$ of the Lagrangian multiplier problem is always a lower bound on the optimal objectivef unction value of the problem (P) .(i.e., $L^* \leq  z^*​$). 

上述几个量之间的关系：
$$
L(\mu) \leq L^{*} \leq z^{*} \leq c x
$$

### 一个例子

这里以一开始的最短路问题为例。
$$
L(\mu)=\min \left\{c_{P}+\mu\left(t_{P}-T\right) : P \in \mathscr{P}\right\}
$$
这里做了一些简化，因为我们不需要把路径守恒约束放到拉格朗日函数中，这样，原问题解的形式可以用路径来表达，这里一条路径$p$表示一系列$x$的取值。通过枚举所有路径 $p$ 可以得到所有 $c_{P}+\mu\left(t_{P}-T\right)$ 的取值。

![1558340610162.png](https://upload-images.jianshu.io/upload_images/11414937-8a902e35bbcf08ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


这样可以作出$L(\mu)$的图像：

![1558341703881.png](https://upload-images.jianshu.io/upload_images/11414937-661122fe9ddf8ec3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 3.次梯度法 Bubgradient Optimization Technique 

>梯度法（爬山法）
>$$
>  \lim _{\theta \rightarrow 0} \frac{f(x+\theta d)-f(x)}{\theta}=\nabla f(x) d
>$$
>选取方向$d$使得$\nabla f(x) d>0$，则$d$就是“上山”方向。
>

次梯度法核心思想：不断按照一个迭代规则移动$\mu​$
$$
\mu^{k+1}=\mu^{k}+\theta_{k}\left(\Delta x^{k}-b\right)
$$

* $x^k$是第$k$次迭代中任意一个解。

在使用这个方法的时候，步长$\theta_{k}$的选择较为重要。如果步长太小，算法会卡在一个地方不无法收敛；如果太大，则会漏掉最优解并且可能在两个或多个非优解之间来回。所以通过设置$\theta_{k} \rightarrow 0 $ 和 $\sum_{j=1}^{k} \theta_{j} \rightarrow \infty$ 使得算法在这两种极端情况中取一个平衡点。

### 牛顿法(Newton's method)

### 不等式情况

$$
\mu^{k+1}=\left[\mu^{k}+\theta_{k}\left(\mathscr{A} x^{k}-b\right)\right]^{+}
$$

## 4.割平面方法 

​        根据上述定义，我们引入辅助变量 $w$, 考察拉格朗日乘子问题。
$$
Max \ w \\
s.t. w \leq c x^{k}+\mu\left(Ax^{k}-b\right) \quad \text { for all } k=1,2, \ldots, K\\
\mu \geqslant  0
$$

这是一个决策变量是$w$和$\mu$的线性规划问题。接下来两章的内容是如何设计算法求解此问题得到 $\mu$。

割平面的基本思想是，我们不需要遍历所有的$X=\{x^{1}, x^{2}, ...,x^K\}$，而是从某一个 $x$ 开始，每一次增加一个$x$(也就是增加一个约束)。即，在第 $k$ 次迭代中，我们要求解如下问题：

$$
Max \ w \\
s.t. w \leq c x^{i}+\mu\left(\mathscr{A} x^{i}-b\right) \quad \text { for all } i=1,2, \ldots, k-1
$$
考虑此问题的对偶形式：
$$
{{\text{ minimize }}\sum\limits_{i = 0}^{k - 1} {{\xi ^i}} \left( {q\left( {{\lambda ^i}} \right) - {\lambda ^i}^\prime {g^i}} \right)}  \\ 
   {{\text{ subject to }}\sum\limits_{i = 0}^{k - 1} {{\xi ^i}}  = 1,\quad \sum\limits_{i = 0}^{k - 1} {{\xi ^i}} {g^i} = 0}  \\ 
   {{\xi ^i} \geqslant 0,\quad i = 0, \ldots ,k - 1}  \\
$$

## 5. 参考文献

1. AHUJA. 1993. NETWORK FLOWS Theory, Algorithms,and Applications



