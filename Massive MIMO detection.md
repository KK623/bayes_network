[TOC]

# 模型

$$
\mathbf{y=Hx+n}
$$

 目的:==在得到$\mathbf{y}$时，推测出$\mathbf{u}$。==

调制方式：$\Omega$,里面有K个符号

---

# 检测准则

## 最大后验(MAP)

> 最大后验：P(H|E)，E是evidence/Data，是已知的。后验是H的函数  [Bayes interfece][https://en.wikipedia.org/wiki/Bayesian_inference]

$\hat{\mathbf{x}}_{\rm MAP}=\arg \max\limits_sP(x|y)$

## 最大似然(ML)

$\hat{\mathbf{x}}_{\rm ML}=\arg \max\limits_sP(y|x)$

## 最小均方误差(MMSE)

$\hat{\mathbf{x}}_{\rm MMSE}=\arg \min\limits_s||\mathbf{x}-\hat{\mathbf{x}}||$

针对MMSE的推导过程，**待补充**

# 基于MMSE的算法

## AOR-famlily(显式)

待补充

## SD-family(隐式)

待补充

# 基于ML的算法

## Sephere-decoding

# 基于MAP的算法

## EP

## AMP

##  BP

###  	图模型：

![image-20201216142856077](Massive MIMO detection.assets/image-20201216142856077.png)

### 	推理过程

$$
\begin{aligned}
p(x_i|H,y)&=\sum_{\mathbf{x}\backslash x_i} p(x_1,x_2,\cdots,x_{N_t}|H,y)\\
\end{aligned}
\\
$$

> 上式是联合概率推导边缘概率公式而来的

从symbol nodes(SN)到observation nodes(ON)传递的是先验概率

从ON到SN传递的是后验概率

首先，将system model从复数域，变为实数域。

> 牵扯到向量和矩阵的复数域到实数域映射。

实数域下

1. $\mathbf{y}$尺寸为$2N_r \times 1$

2. $\mathbf{H}$尺寸为$2N_t\times 2N_r$

3. $\mathbf{x,n}$尺寸均为$2N_t \times 1$
4. $\Omega$ 变为$\{ (-\sqrt{Q}+1),\cdots,-1,1,\cdots,(+\sqrt{Q}-1) \}$

> ==idea:有没有多帧共同处理的可能性？==

#### SN端

计算先验概率的LLR：
$$
\mathbf{\alpha}^{(l)}_{s_i\rightarrow y_j}=\{\alpha^{(l)}_{i\rightarrow j}(s_1),\alpha^{(l)}_{i\rightarrow j}(s_2),\cdots,\alpha^{(l)}_{i\rightarrow j}(s_{\sqrt{Q}-1})\}
$$
这是从第$i$个SN到第$j$个ON传递的信息, 

==$i=1,2,\cdots,N_t$==

==$j=1,2,\cdots,N_r$==

其中每个分量计算：
$$
\alpha^{(l)}_{i\rightarrow j}(s_k)=\ln\frac{p^{(l)}(x_i=s_k)}{p^{(l)}(x_i=s_0)}
$$
也就是对于对于第$i$个SN(用户)，它发射的这个symbol等于$s_k$的LLR，因此每个i，有$\sqrt{Q}-1$个LLR，作为LLR向量进行传递

