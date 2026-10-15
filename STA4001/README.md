# STA4001 第二、三章：概念与历年 Mid 逐题精讲

7 册、46 页 PDF，同时提供可直接阅读公式的 Markdown。内容按“题目在说什么 → 第一反应 → 核心公式 → 推导 → 考场写法 → 易错点”展开，覆盖 5 套不同年份/版本的 Mid 中与 Markov Chain、Poisson Process 相关的 **19 道大题、72 个编号小问**。2024 Q3(a)、Q3(b) 分成两个教学单元，因此共有 20 个逐题教学单元。

## 阅读顺序

| 册 | 内容 | PDF | Markdown |
|---|---|---|---|
| 1 | Markov Chain：状态、矩阵、通信类、周期、平稳与极限、三种首步分析 | [4 页](pdf/01_MarkovChain_概念与方法.pdf) | [在线阅读](markdown/01_MarkovChain_概念与方法.md) |
| 2 | Poisson Process：指数竞争、计数与等待、thinning、条件到达、复合 Poisson | [4 页](pdf/02_PoissonProcess_概念与方法.pdf) | [在线阅读](markdown/02_PoissonProcess_概念与方法.md) |
| 3 | 2022 Fall Q1–Q4，18 个编号小问 | [8 页](pdf/03_2022Mid_逐题精讲.pdf) | [在线阅读](markdown/03_2022Mid_逐题精讲.md) |
| 4 | 2023 Fall Q3–Q5，14 个编号小问 | [6 页](pdf/04_2023Mid_逐题精讲.pdf) | [在线阅读](markdown/04_2023Mid_逐题精讲.md) |
| 5 | 2024 Fall Q1–Q4，17 个编号小问 | [9 页](pdf/05_2024Mid_逐题精讲.pdf) | [在线阅读](markdown/05_2024Mid_逐题精讲.md) |
| 6 | 2025 Spring Mid Q1、Q3–Q5，12 个编号小问 | [7 页](pdf/06_2025SpringMid_逐题精讲.pdf) | [在线阅读](markdown/06_2025SpringMid_逐题精讲.md) |
| 7 | 2025 Spring Sample Q1、Q3–Q5，11 个编号小问 | [8 页](pdf/07_2025SpringSample_逐题精讲.pdf) | [在线阅读](markdown/07_2025SpringSample_逐题精讲.md) |

编号小问按实际作答的末级编号统计。例如 2024 Q3(a) 包含 (i)–(iii)，计为 3 问，Q3(b) 另计 1 问；一个编号小问同时问两个数值时仍计为一个，不通过拆句增加题量。

## 题目定位与去重

| 原始文件 | 本次覆盖 | 原 PDF 页码 |
|---|---|---|
| midterm_2022_solutions.pdf | Q1、Q2、Q3、Q4 | 1；2；2–4；4–5 |
| 2023_Fall_Midterm.pdf | Q3、Q4、Q5 | 1–2；2–3；3–5 |
| Midterm.pdf | 与上一行同一套 2023 试卷的另一个整理版本，核对用，不重复计题 | 1–5 |
| midterm2024-solution.pdf | Q1、Q2、Q3(a)、Q3(b)、Q4 | 1–2；2；2–3；3；3–4 |
| midterm_sol_2025Spring.pdf | Q1、Q3、Q4、Q5 | 1；2–3；3–4；4 |
| midterm_STA4001_sample1.pdf | Q1、Q3、Q4、Q5 | 1–3；3–5；5–7；7 |

2023 Q1、Q2，2025 Spring Mid Q2，以及 2025 Spring Sample Q2 主要属于第一章概率基础，未作为本次第二、三章题目。2025 Spring Mid Q1 是复合 Poisson 随机和，跨越第一章条件期望与第三章内容，因此纳入。2025 Sample Q5 使用三元组链和长期状态收益，纳入 Markov Chain 的应用。

## 课件依据

下载入口：[LGUHub STA4001 课程资料](https://lguhub.cn/course/STA4001)。

- 2026 秋：CHEN Xinyun，2DTMC.pdf，Discrete Time Markov Chain Part I，26 页。
- 2025 春：CHEN Xinyun，2DTMC02_20250311.pdf，Discrete Time Markov Chain Part II。
- 2025 春：CHEN Xinyun，3Poisson_20250408.pdf，Poisson Process。
- 2024 秋：ZHANG Hailun 资料批次中的 slides-chap2(1).pdf、slides-chap3.pdf。

旧版 Part II 文件首页也印有“Chapter 3”，与 Poisson 文件的章号重复。这里按主题将 Part I/II 一并用于 Markov Chain，再将 Poisson 单列；没有把跨版本的首页编号当作本学期统一目录。带批注版本用于核对课程范围，讲义不声称完整转录每一处手写内容。

原始 PDF 已下载到本地课程文件夹；本仓库仅收录重新生成的教学讲义与 Markdown 源稿，不上传原始课件、原试卷。

## 需留意的原材料问题

- 2023 的两个整理版本对高速公路题 Q5(c)–(e) 给出不一致结果。讲义明确保留条件 N(1)=2 后重新推导。
- 2025 Spring Mid 四循环题的答案文字有 p31/p30 笔误；六状态题的路径文字起点也与题面不同，已按矩阵和真实起点解释。
- 2025 Sample Q3 的 Bernoulli 两种概率都写成 p；讲义说明字面含义与原解采用的 p、1−p 模型。
- 2025 Sample Q4 的初始状态 3 不在状态空间 {0,1,2} 中。讲义先指出原小问不合法，再给合法起点下的修正版结论。
- 2025 Sample Q5 的开头下标未完整定义，且相邻峰值指标并不独立。讲义说明有限初始项处理，并补出长期平均收敛的证明。
- 维修链与随机和题说明所采用的事件顺序、独立性前提；不把题面省略的假设悄悄当作已给定。

所有讲解与计算为学习用途的重新推导，不以旧卷规则代替本学期考试要求。
