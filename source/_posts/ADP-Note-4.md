---
title: ADP读书笔记（四）--施工中
date: 2017-11-10 14:32:00
tags: ADP
mathjax: true
---

这一篇笔记中涉及了原书的第六章内容。

# 第六章 策略（Policies)

&emsp;&emsp;也许在动态规划中最广泛运用也最少被了解的就是策略(Policy)了。一个简单的对策略的定义是

(**Definition 6.0.1**) A policy is a rule (or function) that determines a decision given
the available information in state $S_t$
策略就是在给定了可用信息下进行决策的规则（或者是函数）。

&emsp;&emsp;策略这个概念最大的问题就是它指的是根据一个状态(state)得到一个行动(action)的所有方法。*所以对于不同计算需求的不同问题，它包含了很广的算法策略。* 它包含这动态规划帽子下最大范围的问题，所以在讨论的时候我们要规定使用的策略种类，以及对于一个决策最好的策略种类。

&emsp;&emsp;本章中，主要考察四种策略：

**短视策略（Myopic policies）** 
These are the most elementary policies. They optimize costs/
rewards now, but do not explicitly use forecasted information or any direct
representation of decisions in the future. However, they may use tunable
parameters to produce good behaviors over time.

短视策略是最基本的策略。它仅优化当前的回报，不显示地使用预测信息或者任何直接代表未来决策表达。通常它需要调整才能在运行得比较好。

**远视策略（Lookahead policies）**
>These policies make decisions now. They explicitly optimize over some horizon by combining an approximation of future information, with an approximation of future actions.

**策略函数近似（Policy function approximations）**
>These are functions which directly return an
>action given a state, without resorting to any form of imbedded optimization,
>and without directly using any forecast of future information.

**值函数近似（Value function approximations）**
>These policies are often referred to as greedy
>policies. They depend on an approximation of the value of being in a future
>state as a result of a decision made now. The impact of a decision now on
>the future is captured purely through a value function that depends on the
>state that results from a decision now.


[有疑问！]**策略函数近似** 与 **值函数近似** 的区别 

We use this phrase （i.e. 值函数近似）to emphasize the symmetry between approximating the value of being in a state, and approximating the action we should take given a state. 

&emsp;&emsp;近视策略是最简单的，远视策略虽然显示地考虑了每个决策的结果，但是计算量通常非常的大。所以就需要采用近似的方法。用的最多的近似是构造关于决策前状态或者后状态的近似值函数$\bar V \left( s \right)$ 。
$$
{A^\pi} \left( {S_t} \right) = \mathop{arg \; max}\limits_{a}  {\left( {C_t} \left( {S_t},{a} \right) + \bar V \left( S^{M,a} \left( {S_t,a} \right)  \right)  \right)}
$$

&emsp;&emsp;当我们要用**值函数近似** 时， $\pi$ 表示 在一簇近似函数 $\Pi $ 中的一个函数，例如 $\bar V \left( s \right) = \theta_0 + \theta_1 s + \theta_2 s^2$。

&emsp;&emsp;当然我们也可以不使用内嵌的 $max$ 符号，直接给出一个 ${A^\pi} \left( {S_t} \right)$ 来。我们可以认为$\bar V \left( S_t^a \right)$ （ 这里 $S_t^a = S^{M,a} \left( {S_t,a} \right)$  ）是关于下一时刻状态 $S_t^a$ 的近似函数。同时，我们可以认为 ${A^\pi} \left( {S_t} \right)$ 是关于当前状态 $S_t$ 的近似函数。

&emsp;&emsp;直接给出决策的方式：

&emsp;&emsp;**Lookup tables**   这种方式比较特殊所以单独拿出来讲

&emsp;&emsp;**Parametric representations**

&emsp;&emsp;**Nonparametric representations**



## 6.1 短视策略 MYOPIC POLICIES




















