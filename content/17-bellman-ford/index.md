+++
title = "Bellman-Ford 算法"
lecture = 17
slug = "17-bellman-ford"
status = "draft"
source_kind = "notes"
source_url = "https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/mit6_006f11_lec17/"
source_title = "Lecture 17: Bellman-Ford"
output_mode = "explanation"
+++

第 15 讲搭好了通用骨架，把「按什么顺序挑边」留成空位；第 16 讲填上第一种填法，也就是 Dijkstra，代价漂亮但要求权重非负。这一讲填第二种：把所有边老老实实松弛 \(|V|-1\) 轮。它慢一些，却允许负权，并且把第 15 讲留下的那句话兑现 —— 有负权边时，算法要负责把负环找出来。讲义自己的标题是「Shortest Paths III: Bellman-Ford」。

## 一、这一讲要解决什么：记号里多出一种情况

讲义先复习了路径与路径权重：路径是[[term:vertex]]的序列 \(p = \langle v_0, v_1, \dots, v_k \rangle\)，相邻两点之间有边；路径的[[term:weight]]是各边之和。然后给出[[term:shortest-path]]距离函数的定义，讲义的这次定义里多了第三种结果：

> 原文：Shortest path weight from u to v is δ(u, v). δ(u, v) is ∞ if v is unreachable from u, undefined if there is a negative cycle on some path from u to v.

读法是三种情况各有各的写法：能走到就是某个最小的数；走不到写无穷大；而**只要某条从 \(u\) 到 \(v\) 的路上带[[term:negative-cycle]]，这个距离就没有定义**（可以绕着环走任意多圈，让权重一路往下掉）。

第 15 讲把负权边与负环分开说过，这一讲把它们写进了定义本身：没有定义与无穷大不是一回事，前者连数都不是，后者是一个很大的数。

![距离的三种结果：能走到是一个数，走不到是无穷大，路径上有负环则没有定义](figures/bf-delta-undefined.svg)

这张图的意义在于把三种情况并列：前两种都能用数表达，第三种连数都没有。

## 二、通用骨架与两个坏消息

讲义把第 15 讲那个骨架又写了一遍，而这次结尾那句话值得单独看：

> 原文：until you can't relax any more edges or you're tired or . . .

这句玩笑背后是一个真实的问题：**这个「until」没有给出任何上界**。讲义紧接着给两个坏消息。

第一个是终止性：

> 原文：Termination: Algorithm will continually relax edges when there are negative cycles present.

有负环时会一直松弛下去，算法根本停不下来。第二个是代价：边挑得不好，这个过程可能跑指数时间。讲义用的还是那张分层图，出边的权重依次是 4、2、1，而这一次它把两个式子写在了一起：\(T(n) = 3 + 2T(n-2)\) 与 \(T(n) = \theta(2^{n/2})\)。

**那张分层图与那个递推式与第 15 讲是同一个例子**：第 15 讲把它写成 \(T(n+2) = 3 + 2T(n)\)，这里写成 \(T(n) = 3 + 2T(n-2)\)，两者只是同一条递推式的两种写法；指数结论 \(T(n) = \theta(2^{n/2})\) 两讲一致。

![有负环时通用骨架不会终止：每一轮都还能松弛某条边，距离一路往下掉](figures/bf-nontermination.svg)

这张图说明「停不下来」这件事的形状：不是跑得慢，而是根本没有终点。

## 三、Bellman-Ford：把每条边松弛固定轮数

坏消息的根源在于「挑到什么时候停」没有规定。Bellman-Ford 的解法非常直接：**不去挑，把所有边都松弛固定轮数**。

> 原文：Bellman-Ford(G, W, s): Initialize(); for i = 1 to |V| − 1: for each edge (u, v) ∈ E: Relax(u, v); for each edge (u, v) ∈ E: do if d[v] > d[u] + w(u, v) then report a negative-weight cycle exists

三段结构：先初始化；然后把每条[[term:edge]]都[[term:relaxation]]一遍，这样的「一整轮」做 \(|V|-1\) 轮；最后再扫一遍所有边，**只要还有边能被松弛，就说明存在负权环**。

> 原文：At the end, d[v] = δ(s, v), if no negative-weight cycles.

到这里，第 15 讲留下的那条义务就兑现了：算法不但给出距离，还在最后一轮显式地检查负环。用 Python 写，这个骨架比 Dijkstra 还短：两个嵌套的循环，加一次收尾扫描。

![Bellman-Ford 的三段：初始化、把每条边松弛 |V|−1 轮、最后再扫一遍以报出负环](figures/bf-algorithm.svg)

图上第三段与前两段是分开的：前两段算距离，第三段只做一件事，就是判断有没有负环。

## 四、为什么 \(|V|-1\) 轮就够

讲义给的定理是一句条件句：

> 原文：Theorem: If G = (V, E) contains no negative weight cycles, then after Bellman-Ford executes d[v] = δ(s, v) for all v ∈ V.

证明的思路很值得记住，因为它解释了「轮数」这个数是从哪来的。取任意一个顶点 \(v\)，再取一条从源点到 \(v\) 的最短路径，并且在所有最短路径里挑边数最少的那一条 \(p = \langle v_0, v_1, \dots, v_k \rangle\)。因为[[term:graph]]里没有负环，这条路径一定不重复顶点，于是 \(k \le |V| - 1\)。

然后一轮一轮看：

> 原文：After 1 pass through E, we have d[v1] = δ(s, v1) … After i passes through E, we have d[vi] = δ(s, vi). After k ≤ |V| − 1 passes through E, we have d[vk] = d[v] = δ(s, v).

读法是：第一轮一定会松弛边 \((v_0, v_1)\)，所以 \(v_1\) 定下来；第二轮轮到 \((v_1, v_2)\)，于是 \(v_2\) 定下来；依此类推，第 \(k\) 轮就把 \(v_k = v\) 定下来。而 \(k\) 最多是 \(|V|-1\)，所以做满 \(|V|-1\) 轮就够了。

讲义在这里明确点了一句出处：这一步用到了**第 16 讲的[[term:optimal-substructure]]与安全引理**（那一讲的参考读物是 CLRS 的 24.2 到 24.3 节）。这也说明三讲之间是同一套地基：Dijkstra 靠「松弛安全」证明「取出来就定稿」，Bellman-Ford 靠同一个安全引理证明「第 i 轮能定下第 i 个顶点」。

![为什么 |V|−1 轮够：第 i 轮能让最短路径上的第 i 个顶点定稿，而这条路径最多有 |V|−1 条边](figures/bf-correctness.svg)

这张图是「一轮推进一格」的画面版：轮数与路径长度一一对应，而路径长度不会超过顶点数减一。

## 五、推论：轮数用完还不收敛，就是负环

定理的前提是「没有负环」，那么如果把前提去掉，算法还能给出信息吗？讲义给了一个推论：

> 原文：Corollary: If a value d[v] fails to converge after |V| − 1 passes, there exists a negative-weight cycle reachable from s.

证明也很短：\(|V|-1\) 轮之后如果还能找到一条可松弛的边，说明当前那条「最短路」重复经过了某个顶点，也就是**不是简单路径**；而这条带环的路径比任何简单路径都轻，于是那个环只能是负环。

**这正是第三段收尾扫描的意义**：它把「算不出正确答案」这件事，变成了一个可以报告的结论。

![推论：|V|−1 轮之后还能松弛，说明当前路径重复经过了顶点，那个环一定是负环](figures/bf-corollary.svg)

这张图把证明的两步串起来：先由「还能松弛」推出路径不简单，再由「带环的路径更轻」推出那个环是负环。

## 六、5 分钟 6.006：指数与多项式的分界

这一讲讲义里最特别的一段是它自己标成「5-Minute 6.006」的那张图，配上一句很直白的话：

> 原文：Figure 4 is what I want you to remember from 6.006 five years after you graduate!

那张图把两种递推式并排放在一起：一种是 \(T(n) = C_1 + C_2 T(n - C_3)\)，另一种是 \(T(n) = C_1 + C_2 T(n / C_3)\)。前者里 \(C_2 > 1\) 就是麻烦，讲义给它的标签是「Divide & Explode」；后者只要 \(C_3 > 1\)，即使 \(C_2 > 1\) 也没关系，标签是「Divide & Conquer」。

把它与这一讲的两个算法对起来看就明白了（这一层对应是我们补的）：**通用骨架的病态选边落在那条指数曲线上，而 Bellman-Ford 的 \(\Theta(VE)\) 落在多项式这一侧。** 差别不在于聪明的技巧，而在于「一共要做多少次松弛」这件事有没有上界。

![指数与多项式的分界：问题缩得很慢就危险，缩得快就安全（讲义说这张图要记五年）](figures/bf-exponential-vs-polynomial.svg)

这张图的分界线画在两个递归项上：一个让规模只减一点，一个让规模按比例缩小。

## 七、最长简单路径：为什么不能把权重取反

讲义最后给了一个反例方向的运用，说明 Bellman-Ford 不能拿来解另一个问题。先看不带负环的图：

> 原文：Finding the longest simple path in a graph with non-negative edge weights is an NP-hard problem, for which no known polynomial-time algorithm exists.

既然有高效的「最短」，那能不能把所有边的权重取反，再跑一次 Bellman-Ford 来得到最长？讲义说不行：

> 原文：Bellman-Ford will not necessarily compute the longest paths in the original graph, since there might be a negative-weight cycle reachable from the source, and the algorithm will abort.

原因是取反之后可能出现从源点可达的负环，而算法一旦发现负环就会中止，于是最长路径也没算出来。同样的道理，如果原图本身带负环，想求从 \(s\) 到 \(v\) 的最长简单路径也不能用这套办法；讲义还补了一句：最短简单路径问题同样是 NP-hard。

所以这一段的价值不在于算法，而在于划边界：**Bellman-Ford 能处理负权边，但它处理的仍然是「最短」，而不是「最长」。**

![最长简单路径：把权重取反再跑 Bellman-Ford 不行，因为负环会让算法中止](figures/bf-longest-path.svg)

这张图给出的是一条常见的错误思路，以及它为什么在负环面前失效。

## 读完应该能回答

- 距离函数的三种结果分别在什么情况下出现，为什么「没有定义」与「无穷大」不是一回事；
- 通用骨架的两个坏消息各是什么，它们的根源是不是同一个；
- Bellman-Ford 为什么固定做 \(|V|-1\) 轮，这个数字是从哪里来的；
- 最后一轮收尾扫描在做什么，它凭什么能报出负环；
- 为什么把权重取反再跑一遍，得不到最长简单路径。

## 脉络回顾

这一讲是「最短路径三讲」的收尾，三讲合起来是同一个骨架的两次填法。第 15 讲给出骨架本身：初始化加松弛，并把「按什么顺序挑边」留成空位，同时用一个病态例子说明乱挑会慢到指数级。第 16 讲的 Dijkstra 用「每次取当前最小」填这个空位，代价降到 \(\Theta(V \lg V + E)\)，代价是要求权重非负，因为「一进 S 就定稿」这条性质经不起负权边。而这一讲的 Bellman-Ford 用「把所有边都松弛 \(|V|-1\) 轮」填同一个空位，代价是 \(\Theta(VE)\)，换来了对负权的容忍，并且额外给出负环的判定。

要分清的是，两者的取舍不在技巧上，而在有没有用一个可能不成立的前提。Dijkstra 的证明依赖「取出来的顶点不会再被改小」，所以它必须排除负权；Bellman-Ford 不做这个假设，于是它要用「轮数」这个笨办法来保证覆盖到足够长的路径。第 15 讲那条义务也在这里闭合：有负权边时算法要报出负环，这正是收尾扫描那一段的作用。

再往后，图算法会从「单源最短路」转向别的题型，而这一讲最后那段关于最长简单路径的讨论留下了一个新的方向：有些看起来只差一个符号的问题，难度却是 NP-hard。

## 溯源

本讲的内容来自 MIT 6.006 Fall 2011 的 Lecture 17: Shortest Paths III: Bellman-Ford 讲义（6 页 typed notes；第 6 页是 OCW 版权页；讲义自身页眉与标题写作 Shortest Paths III: Bellman-Ford，而 OCW 资源页的标题是 Bellman-Ford，本页 front matter 用后者、正文按讲义内容写）。本讲的事实都能在上述讲义里逐条对上：Lecture Overview 的三项；路径与路径权重的复习、以及 \(\delta\) 的三种结果（能到达、不可达写无穷大、路径上有负环则没有定义）；通用骨架的初始化与主循环、以及那句 `until you can't relax any more edges or you're tired or . . .`；「有负环时算法不终止」与「边挑得不好可能是指数时间」；那张分层图、\(T(n) = 3 + 2T(n-2)\) 与 \(T(n) = \theta(2^{n/2})\)；Bellman-Ford 的三段伪代码、收尾扫描那句 `then report a negative-weight cycle exists`、与「没有负环时 \(d[v] = \delta(s,v)\)」；定理的条件句表述、证明里「取边数最少的最短路径 ⇒ 不重复顶点 ⇒ \(k \le |V|-1\)」这条推理、以及「第 i 轮定下第 i 个顶点」的推进（含它对第 16 讲最优子结构与安全引理的引用）；推论与它的证明（还能松弛 ⇒ 路径不简单 ⇒ 环更轻 ⇒ 负环）；「5-Minute 6.006」那段与 Figure 4 的两种递推式、`Divide & Explode` 与 `Divide & Conquer` 两个标签；以及最长简单路径那两段（NP-hard、取反之后可能遇到可达负环而中止、最短简单路径也是 NP-hard）。

讲义没有写的部分，以下是我们补的：这篇中文讲解本身（讲义是英文提纲），全部配图（讲义里的示意图一律重画，不转载），以及三处展开说明：

1. 「停不下来」的性质说明：不是跑得慢，而是没有终点；
2. 「通用骨架的病态选边落在指数一侧、Bellman-Ford 落在多项式一侧」这个对应关系（讲义只把两种递推式并排画出来，没有点明它与本讲两个算法的对应）；
3. 「三讲是同一个骨架的两次填法」这个收尾说法，以及 Dijkstra 与 Bellman-Ford 的取舍「不在技巧、而在有没有用一个可能不成立的前提」。

另外四处登记：一是这一讲的分层图与递推式**与第 15 讲是同一个例子**，只是递推式写成 \(T(n) = 3 + 2T(n-2)\)（第 15 讲写作 \(T(n+2) = 3 + 2T(n)\)），本页按「同一条递推式的两种写法」处理；二是讲义 Figure 5 那张执行示例只读出两段状态（End of pass 1 与 End of pass 2 (and 3 and 4)）与部分权重（含一条 −3 的负边），具体的 d 值在文本层读不全，所以本页没有复述；三是讲义 Figure 4 那句「毕业后五年还该记住它」是讲师的原话，本页照录；四是讲义把负环检查写成对每条边的一次遍历（不是多轮循环），本页按「再扫一遍所有边」表述。
