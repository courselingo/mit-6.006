# 事实核对 · MIT 6.006 第 2 讲 计算模型与文档距离

- 核对人：非作者（`fig-pruner`。**没有**参与本讲任何一轮写作，也没有与作者 `mit6006-author` 讨论过本讲内容）
- 核对日期：2026-09-29
- 被核对版本：`content/02-models-of-computation-document-distance/index.md`，归一化 SHA256 前16 = **D191F6A3DCE5CBB8**
  （全 64 位 `D191F6A3DCE5CBB886543A03930B81DCCFE02205DEF5E400D7540BB27FBB586D`，14715 B）
  - 归一化 = `path.read_bytes().replace(b"\r\n", b"\n")` 之后再算 SHA256（工作区 CRLF、git 存 LF）
- 源材料（本次实际依据的，逐个列出）：
  1. **6.006 Fall 2011 Lecture 2 typed notes**（8 页；第 8 页是 OCW 版权页）
     - 抓取 URL：<https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/6b9b20992d8c6a0f3f10a34ff7878aa9_MIT6_006F11_lec02.pdf>
     - 本地副本：`_sources/MIT6_006F11_lec02.pdf`（966,515 B，SHA256 前16 `85CC80CEEB145CCB`，本次现抓、运行时只读）
     - 文本层：`_sources/MIT6_006F11_lec02.pdf.clean.txt`（pypdf 按页抽取；SHA256 前16 `FD0C569A261DF5DA`）。**本记录一律用 `p.N` 指 PDF 页码**
  2. **OCW 资源页**：<https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/mit6_006f11_lec02/>（本次现抓；其 `<title>` 逐字为
     `Lecture 02: Models of computation, Python cost model, document distance | Introduction to Algorithms | …`）
  3. **OCW 日历页**：<https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/calendar/>（本次现抓，用于核 `psuedopolynomial` 的出处）
  4. **讲义 Figure 1 的文本坐标**：用 pypdf 解该页 Form XObject 的 `Tm/Td/Tj/TJ` 得到（用于 P1-3；坐标为 XObject 用户空间，y 向上）

## 结论

P0（事实错误）：**2 条** ｜ P1（易误解/依据不足）：**5 条** ｜ P2（措辞）：**5 条**

## P0 · 事实错误

| # | 位置（小节/原文） | 正文说 | 源材料说 | 依据（逐字引用 + 页码/小节） |
| --- | --- | --- | --- | --- |
| P0-1 | 三、指针机（L46） | 「两种模型的关系，讲义只用了一句括注说清：指针机比 RAM 弱，因为它可以在 RAM 上实现出来。**换句话说，RAM 能做的它都能做**，但它能表达的东西更少。」 | 指针机**弱于** RAM：它能做的 RAM 都能做，反过来不成立 | p.2「Pointer Machine」末条：`• weaker than (can be implemented on) RAM`。同一段前一句「指针机比 RAM 弱」是对的，紧接着的这句把包含方向写反了（应是「它能做的 RAM 都能做」）。 |
| P0-2 | 五、文档距离（L81） | 「…一篇长文档只要和另一篇有 99% 的词相同，乘出来的数会很大；而两篇短文档哪怕 10% 的词相同，数也可能更小。**于是「长文更像」这种错觉会盖过真实的重合度。**」 | 长文档**显得更远**（not scale invariant 的后果） | p.5（Document Distance Problem 一节）逐字：`The problem is that this is not scale invariant. This means that long documents with 99% same words seem farther than short documents with 10% same words.`。正文把 d′ 明确定义成**距离**（L73–L75），而它自己刚说长文的数「会很大」⇒ 大写 = 更远；结论句却写成「长文更像」，与源文 `seem farther` 相反。（若把 d′ 当相似度读，本句内部自洽，但那与源文把它叫 distance 的用法矛盾。） |

## P1 · 易误解或依据不足

1. **P1-1 · `algorithm` 的词源（一、L18）**：「algorithm 这个词本身就是他名字的拉丁化。」
   - 源 p.1 的 History 一节只有三行：`Al-Khw¯arizm¯ı "al-kha-raz-mi" (c. 780-850)`、`"father of algebra" with his book "The Compendious Book on Calculation by Completion & Balancing"`、`linear & quadratic equation solving: some of the first algorithms`——**没有**任何词源句。
   - 溯源（L145）把这句所在的一节整体登记为「本讲的事实都能在上述讲义里逐条对上，包括…花拉子米的生卒与著作」，这一句既不是生卒也不是著作，**没有**被列进「讲义没有写、以下是我们补的」那六条。
   - 该说法在通用文献里成立（算法一词经中世纪拉丁语 algorismus 来自其名的拉丁化），但**不在本讲讲义里** ⇒ 应就近标为「讲义外补充」或补出处。
2. **P1-2 · 副标题的三件事（L14）**：「副标题给了三件事：random access machine、Python 的代价模型、以及…document distance。」
   - OCW 资源页 `<title>` 逐字：`Lecture 02: Models of computation, Python cost model, document distance`；讲义 p.1 页眉逐字：`Lecture 2: Models of Computation`；p.1「Lecture Overview」列的是**五条**：`What is an algorithm? What is time?` / `Random access machine` / `Pointer machine` / `Python model` / `Document distance: problem & algorithms`。
   - 副标题第一项是「计算模型」，而 RAM 只是该讲给出的两个模型之一（本页第三节自己还讲了指针机）⇒ 把「计算模型」写成「random access machine」是把两个模型中的一个当成全部，属引称不实。
3. **P1-3 · 讲义 Figure 1 的读法（L20 与 L26 的 alt）**：正文「讲义那张图就是讲这个关系：**编程语言对应程序，计算机对应算法**，而计算模型托在两者之间」；`alt`「**编程语言落在程序上，计算机落在算法上**，计算模型托在中间」。
   - 按 Figure 1 的文本坐标重建版面（p.1，Form XObject）：
     `program (42.3, 76.7)` 与 `algorithm (155.3, 76.5)` 同一行；`programming language (27.9→40.5, 58.7→44.3)` 与 `pseudocode (150.3, 52.5)` 居中一行；`computer (39.0, 22.5)` 与 `model of computation (153.8→145.0, 29.0→14.6)` 在底行；图例 `analog (101.3, 98.5)` 在顶部正中，`built on top of (234.8→240.5, 68.5→54.1)` 在最右侧。
   - ⇒ 与 `computer` 同一行并列的是 `model of computation`（**不是** `algorithm`）；`model of computation` 与 `algorithm` 同一列、位于它**下面**（不是「托在两者之间」）。正文读出来的两组配对（语言↔程序、计算机↔算法）与源图版面不符。
   - **限制**：箭头端点不在文本层里，我只核了六个标签的坐标与两个图例的位置，**没有**核箭头方向；因此本条的结论限于「配对与位置」，不涉及 `analog` / `built on top of` 各自连哪两格。
4. **P1-4 · `psuedopolynomial` 的出处写错（溯源 L156）**：「讲义第 21 页标题里的 `psuedopolynomial` 是 OCW 原文的拼写」。
   - 拼写本身**成立**：我现抓 OCW 日历页，第 21 讲那一行逐字为 `String subproblems, psuedopolynomial time; parenthesization, edit distance, knapsack`。
   - 但出处不是「讲义第 21 页」：本讲讲义共 **8 页**（p.8 是 OCW 版权页），第 21 页并不存在；该字样在 **OCW 日历页第 21 讲**那一行的标题里。本项目自己的 `docs/lecture-manifest.md` L71 也写「**标题逐字取自日历页 TOPICS 列**（含原文拼写，例如第 21 讲的 `psuedopolynomial` 保持原样）」。
   - ⇒ 读者按「讲义第 21 页」去核对会找不到，应改为「OCW 日历页第 21 讲的标题」。
5. **P1-5 · 溯源第五条里的「第一步」（L153）**：「讲义把**第一步**的排序代价写成 O(k log k · |word|)，本篇改用与全文长度一致的 O(|doc| log |doc|)」。
   - 源把该式放在第 **(2)** 步：p.6 `(2) sort word list … ← O(k log k ·|word|) where k is #words`；本页正文（L100）也把它放在第二步「计数」的两条路线之一；**第一步（拆词）在源与本页都没有排序**。
   - 若「第一步」是指两条计数路线里的「第一条（先排序）」，措辞应写「第一条路线」，否则读者会去第一步找排序代价。

## P2 · 措辞

1. **引文少了一个词**：L38「讲义写的是 \(w \ge \lg(\text{memory size})\)」，源 p.2 逐字为 `• What's a word? w ≥ lg (memory size) bits`——原文末尾的 `bits` 被略去。解释方向（字长要够放下一个内存地址）不受影响。
2. **w.h.p. 那一段（L105）**：「字典的查找与插入是**期望意义下 Θ(1)**：期望是平均值，高概率是几乎必然…」源两处都只写概率式：p.4 `D[key] = val / key in D → θ(1) time w.h.p.`、p.6 `O(|doc|) w.h.p.`——**源没有「期望 Θ(1)」这种说法**。「期望 Θ(1)」是我们的补充（溯源第 3、4 条已登记），但正文就近没有标明，读起来像源同时给了两种界。建议把这半句标成我们的补充。
3. **Python 代价清单的完整性（L57–L63）**：正文列了 (a) `L.append`、(b) `L = L1 + L2`、(c) `L.extend`、(d) 切片、(e) `x in L / L.index / L.find` 五项；源 p.3–p.4 还列了 (f) `len(L) → θ(1)`、(g) `L.sort() → θ(|L| log |L|)`，以及 tuple/str、dict、set、heapq、long 五类。正文说的是「讲义把常见的几个列了出来」，字面不错，但紧接着说「这份清单值得背下来」，读者可能以为这就是全部。
4. **「讲义的两张 Figure」（溯源 L147）**：源确有 2 张**编号** Figure（p.1 `Figure 1: Algorithm`、p.5 `Figure 2: D1 = "the cat", D2 = "the dog"`），字面没错；但源还有未编号的示意图（p.2 的 RAM 大数组与 `}`、p.3 的指针机节点 `val/prev/next`），本页也重画了它们。建议写「讲义的两张编号 Figure 与若干示意图一律重画」。
5. **「耗时能差出好几个数量级」（L12）**：这是我们的话，源没有给语言/机器差异的量级（源的理由是「先约定代价才能谈复杂度」）。可以注明：讲义自己的实测表（228.1 秒 → 0.2 秒，p.7）确实跨了 3 个数量级，本句的量级感来自那张表。

## 已逐条回源、未发现问题的（抽样清单，供复核者不必重做）

- 8 个版本的耗时**逐字一致**（p.7）：`228.1 / 164.7 / 123.1 / 71.7 / 18.3 / 11.5 / 1.8 / 0.2`，以及每版一句改动说明（`words = words + words on line`、`words += words`、`(3)' … with insertion sort`、`(2)' but still sort to use (3)'`、`split words via string.translate`、`merge sort (vs. insertion)`、`(3) (full dictionary)`、`whole doc, not line by line`）。
- 两篇测试文本的规模与机器配置**逐字一致**（p.7）：`268,778 chars/49,785 words/3354 uniq`、`1,031,470 chars/182,355 words/8534 uniq`、`Pentium 4, 2.8 GHz, C-Python 2.62, Linux 2.6.26`（2.62 = 2.6.2）。
- **Salton 1975**（Lead 点名的优先项）：p.5 逐字 `This approach was introduced by [Salton, Wong, Yang 1975].` ✅ 正文 L91 的归属正确。
- RAM：大数组建模、`Θ(1) registers (each 1 word)`、三条 `In Θ(1) time` 操作（load / compute `+,-,*,/,&,|,^` / store）、`w ≥ lg (memory size) bits`、`assume basic objects (e.g., int) fit in word`、`unit 4 in the course deals with big numbers`（p.2）✅ 全部一致。
- 指针机：`dynamically allocated objects (namedtuple)`、`O(1) fields`、`field = word … or pointer to object/null`（p.2）✅ 一致（「弱于 RAM」的方向见 P0-1）。
- Python 模型 (a)–(e) 的代价式与 `L[i] = L[j] + 5 → Θ(1)`、`x = x.next → Θ(1)`（p.3–p.4）✅ 逐条一致；`L.append` 的 `via table doubling [Lecture 9]` ✅（正文「第九讲」）。
- 文档距离：`d'(D1,D2) = D1 · D2`、`d''(D1,D2) = D1·D2/(|D1|·|D2|)`、`d = arccos(d'')`、`An angle of 0◦ means the two documents are identical whereas an angle of 90◦ means there are no common words`（p.5）✅ 一致；`D1 = "the cat", D2 = "the dog"` ✅。
- 三步算法：`re.findall` 可能指数级 + 逐字符 `Θ(|doc|)`（p.6）✅；排序路线 `O(k log k ·|word|) where k is #words` ✅（正文的 `O(|doc| log |doc|)` 是它声明的记号统一）；字典路线 `O(|doc|) w.h.p.`（p.6）✅；点积两种写法 `O(k1 · k2)` 与归并（p.6）✅；`via hashing [Unit 3 = Lectures 8-10]` ✅（正文「第三单元」）。
- 溯源 L145 的「8 页，其中第 8 页是 OCW 版权页」✅（p.8 逐字为 `MIT OpenCourseWare / http://ocw.mit.edu / 6.006 Introduction to Algorithms / Fall 2011 / For information about citing these materials or our Terms of Use…`）。

## 我核不到的（诚实记录）

- **讲义 Figure 1 的箭头方向**：Form XObject 的文本层只有标签，没有路径几何；我**无法**核 `analog` 与 `built on top of` 各自连接哪两格。P1-3 只依赖六个标签的坐标与两个图例的位置。
- **「这门课的教材 CLRS 里，绝大多数算法就是在这个模型下分析的」（L24）**：源 p.1 **没有** CLRS 字样（CLRS 出现在第 1 讲）。本页溯源 L156 已自行登记「讲义本身没有写」⇒ 归属已标明，我**不判错**，也没有去核「绝大多数算法」这个比例（讲义外主张）。
- **「本讲的讲次顺序与模块号沿用第一讲的说明」（L156）** 与 **「第九讲/第三单元/第四单元」的具体内容**：我只核到源里确实写了 `[Lecture 9]`、`[Unit 3 = Lectures 8-10]`、`unit 4`；这些讲次/单元**内部**讲了什么，不在本讲范围内，未核。
- **机检指标与图内像素**：本记录不重跑 `audit_content.py` / `check_figures.py`，也不渲染 SVG 量墨迹（那是视觉复核与机检的活）。
- **检索范围与词**（否定性结论一律附范围）：
  - 全文范围：本讲 **8 页全部**逐页读完（`_sources/MIT6_006F11_lec02.pdf.clean.txt`，7438 B）。
  - P1-1：在本讲全文内找词源表述（`algorithm` 出现于 p.1 标题与 bullet，周边无 Latin/词源句）。
  - P1-4：抓 OCW 资源页与日历页各一次（均首次 200），逐字比对 `pseudo|psuedo`；工作区全仓 grep `psuedopolynomial|pseudopolynomial` 只命中本页与 `docs/lecture-manifest.md`（即：工作区里**没有**留存的日历页副本，本条的出处是我这次现抓的）。
  - P1-3：解 p.1 的 Form XObject `/Fm0`（BBox `[10.379, 10.6, 276.209, 109.885]`）取坐标。

---

**核对人声明**：本记录只覆盖开头钉住的基线版本（前16 `D191F6A3DCE5CBB8`）。页面若再改动，结论不自动成立。本记录**不修改**任何正文、配图或 `status`——`status` 由 Lead 处理。
