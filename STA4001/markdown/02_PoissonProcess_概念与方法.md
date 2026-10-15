# STA4001 第三章：Poisson Process，把“数量”和“等待”连起来

这一册的核心问题：随机事件不断发生时，如何在计数、到达时刻、分类计数和仍在系统中的人数之间转换？

学习路线：指数寿命 → 无记忆性与竞争 → Poisson 计数 → 第几次到达 → thinning → 条件到达时刻 → 随机和与在系统人数。第二章负责离散步的状态；第三章负责连续时间中随机事件的发生。

课件依据：3Poisson_20250408.pdf（2025 春，CHEN Xinyun，带课堂批注）以及 slides-chap3.pdf（2024 秋，58 页）。后者第 2 页列出指数分布、Poisson 过程、间隔与等待时间、条件到达时刻、进一步性质、复合 Poisson 与非齐次 Poisson。各年题中的时间单位与率参数以题面为准。

## 1. 指数分布中的参数是 rate

$X\sim\operatorname{Exp}(\lambda)$ 表示寿命或等待时间，其中 $\lambda>0$ 是每单位时间的率：

$$
f_X(x)=\lambda e^{-\lambda x},\quad
P(X>x)=e^{-\lambda x},\quad
E[X]=1/\lambda,\quad
\operatorname{Var}(X)=1/\lambda^2.
$$

密度用于区间概率的积分；尾概率 $P(X>x)$ 直接表示“等到 $x$ 还没发生”。$\lambda$ 是率，不是均值；率越大，平均等得越短。若率单位是每分钟，$1/\lambda$ 的单位就是分钟。

## 2. 无记忆性：已经等过的部分不再计入剩余等待

$$
P(X>s+t\mid X>s)=\frac{e^{-\lambda(s+t)}}{e^{-\lambda s}}
=e^{-\lambda t}.
$$

“已等待 $s$ 以后，还要再等超过 $t$”和“刚开始要等超过 $t$”的概率相同。剩余时间仍是指数分布，但总时间不是凭空变短。

在服务题中，遇到已经服务了一阵的指数服务，剩余服务时间仍服从同率指数分布。独立性条件也必须保留：不能把任意相互关联的寿命都当作独立指数竞争。

## 3. 指数竞争与最小值

独立的 $X_i\sim\operatorname{Exp}(\lambda_i)$ 同时运行，最早发生的时间为 $M=\min_iX_i$。事件 $M>t$ 等价于所有 $X_i>t$，所以

$$
P(M>t)=\prod_ie^{-\lambda_it}=e^{-t\sum_i\lambda_i},
\qquad E[M]=\frac1{\sum_i\lambda_i}.
$$

两个竞争者中第一个先发生的概率为

$$
P(X_1<X_2)=\int_0^\infty
\lambda_1e^{-\lambda_1t}e^{-\lambda_2t}\,dt
=\frac{\lambda_1}{\lambda_1+\lambda_2}.
$$

注意它和 $E[M]$ 是不同的问题：一个问谁先到，一个问何时先到。

## 4. 最大寿命：最后一个坏掉才停机

若三组件串联系统要求全部工作，系统寿命是最小值；并联系统只要至少一个还工作，系统寿命是最大值。

令 $Y=\max(X_1,X_2,X_3)$，则

$$
P(Y\leq t)=\prod_{i=1}^3(1-e^{-\lambda_it}).
$$

用非负随机变量的尾积分公式，比先求密度再积分更短：

$$
E[Y]=\int_0^\infty P(Y>t)\,dt
=\sum_i\frac1{\lambda_i}
-\sum_{i<j}\frac1{\lambda_i+\lambda_j}
+\frac1{\lambda_1+\lambda_2+\lambda_3}.
$$

三个率都等于 $\lambda$ 时，它变成 $11/(6\lambda)$，应大于单个寿命 $1/\lambda$；最小寿命则是 $1/(3\lambda)$。

## 5. Poisson 过程和一段时间内的计数

$N(t)$ 表示从起点到时刻 $t$ 的累计到达数。齐次 Poisson 过程具有独立增量和平稳增量，且

$$
N(t)-N(s)\sim\operatorname{Poi}(\lambda(t-s)),\quad0\leq s<t.
$$

独立增量说不相交时间段的计数独立；平稳增量说分布只依赖区间长度。$N(2)$ 与 $N(5)$ 不是独立，因为前者包含在后者中。

若 $K\sim\operatorname{Poi}(a)$，

$$
P(K=k)=e^{-a}\frac{a^k}{k!},\quad k=0,1,\ldots,\qquad
E[K]=\operatorname{Var}(K)=a.
$$

至少一个到达：$1-P(K=0)=1-e^{-a}$。题目给 rate 为 $\lambda$、区间长为 $t$ 时，代入的均值是 $a=\lambda t$，不是单独的 $\lambda$。

## 6. 第几次到达：时间题改写成计数题

令 $S_k$ 为第 $k$ 次到达的时刻，$W_i=S_i-S_{i-1}$ 为相邻到达间隔。对齐次 Poisson 过程，

$$
W_i\ \text{i.i.d.}\sim\operatorname{Exp}(\lambda),\qquad
S_k=\sum_{i=1}^kW_i,\qquad E[S_k]=k/\lambda.
$$

第 $k$ 次到达还没有发生，等价于累计到达数还不到 $k$：

$$
\{S_k>t\}=\{N(t)\leq k-1\},\qquad
P(S_k>t)=e^{-\lambda t}\sum_{j=0}^{k-1}\frac{(\lambda t)^j}{j!}.
$$

这个写法不需要背 Gamma 密度。Gamma 的参数有 rate 与 scale 两种习惯；本讲义使用 shape $k$、rate $\lambda$。

## 7. Thinning：每个到达独立分类

若每个到达独立地以概率 $p$ 归入 A、以 $q=1-p$ 归入 B，且分类标记与到达过程独立，则

$$
N_A(t)\sim\operatorname{Poi}(\lambda pt),\quad
N_B(t)\sim\operatorname{Poi}(\lambda qt),
\quad N_A,N_B\ \text{相互独立}.
$$

给定总数时却不同：

$$
N_A(t)\mid N(t)=n\sim\operatorname{Bin}(n,p),\qquad N_B(t)=n-N_A(t).
$$

因此“拆分后无条件独立”与“固定总数后负相关”并不冲突。$N_A$ 和总数 $N=N_A+N_B$ 也不独立。

若 $\lambda>0$、$0<p<1$，

$$
\operatorname{Cov}(N_A(t),N(t))=\lambda pt,\qquad
\operatorname{Corr}(N_A(t),N(t))=\sqrt p.
$$

端点 $p=0$ 时 A 计数恒为零，方差为零，Pearson 相关系数没有定义；不能机械写成 0。

## 8. 已知一段时间内到达总数，如何放置到达时刻

给定 $N(t)=n$，到达时刻 $(S_1,\ldots,S_n)$ 的联合分布等于 $n$ 个独立 $\operatorname{Unif}(0,t)$ 的有序统计量。

这里每个有编号的 $S_i$ 不是独立均匀分布，尤其 $S_1$ 是最早到达者。不过对不依赖排序的和，可以改用未排序的独立均匀样本：

$$
E\left[\sum_{i=1}^ng(S_i)\mid N(t)=n\right]
=\frac nt\int_0^tg(u)\,du.
$$

另一个等价的计数结论是

$$
N(s)\mid N(t)=n\sim\operatorname{Bin}(n,s/t),\quad0<s<t.
$$

这是 2022 礼品店题和 2023 高速公路题的关键：前者按早到/晚到分类，后者对到达时刻上的存活概率取平均。

## 9. 随机和与复合 Poisson

令 $G\sim\operatorname{Poi}(a)$ 为组数，每组人数 $Y_i$ 独立同分布，并且与 $G$ 独立。总人数是

$$
S=\sum_{i=1}^{G}Y_i,\qquad S=0\ \text{当 }G=0.
$$

先条件化组数：

$$
E[S\mid G]=G\mu,\quad
\operatorname{Var}(S\mid G)=G\sigma^2.
$$

再使用全期望和全方差：

$$
E[S]=aE[Y],\qquad
\operatorname{Var}(S)=a\{\operatorname{Var}(Y)+(E[Y])^2\}
=aE[Y^2].
$$

最后一个式子中特别容易把二阶矩 $E[Y^2]$ 写成方差。总人数通常不服从普通 Poisson 分布，因为一个组到达时可能同时增加多个人。

## 10. 在系统人数：到达过不等于仍在

到达于时刻 $u$ 的个体，到观察时刻 $t$ 还在系统中的概率为 $P(D>t-u)$，其中 $D$ 是独立停留时间。未条件化的平均在系统人数可以通过小区间求和得到

$$
E[L(t)]=\lambda\int_0^tP(D>t-u)\,du.
$$

若 $D\sim\operatorname{Exp}(\mu)$，

$$
E[L(t)]=\frac{\lambda}{\mu}(1-e^{-\mu t}).
$$

若已经给定 $N(a)=n$，就要把 $(0,a)$ 的旧到达者与 $(a,t)$ 的新到达者分开：

$$
E[L(t)\mid N(a)=n]
=\frac na\int_0^aP(D>t-u)\,du
+\lambda\int_a^tP(D>t-u)\,du.
$$

第一项用条件均匀到达；第二项用独立增量。不能拿未条件化公式直接覆盖“已知前一段恰有几人”的条件。

## 11. 做题前的四个检查

- 问数量还是问时间？数量用 Poisson，时间用指数/Gamma 或转换成数量事件。
- 给的是累计过程还是某个随机总数？只给 $N\sim\operatorname{Poi}(\lambda)$ 不自动提供时间过程。
- 是否给定总数？条件化后往往出现 Binomial 或 Uniform，而不是另一条独立 Poisson 公式。
- 是否有分类、服务、存活？把到达随机性与之后的标记/寿命随机性分开。

看到独立指数竞争，先写“谁的时钟先响”；看到随机项数，先固定项数；看到已知区间总数，先把到达时刻放回区间；看到第 $k$ 次到达，先问“此时计数是否不到 $k$”。
