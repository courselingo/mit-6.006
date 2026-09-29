# 事实核对 · MIT 6.006 第 2 讲 计算模型与文档距离

- 核对人：非作者（`fig-pruner`。**没有**参与本讲任何一轮写作，也没有与作者 `mit6006-author` 讨论过本讲内容）
- 核对日期：2026-09-29（**同日重钉，见文末「重钉」一节**）
- 被核对版本：`content/02-models-of-computation-document-distance/index.md`
  - **旧基线**：归一化 SHA256 前16 = **D191F6A3DCE5CBB8**（全 64 位 `D191F6A3DCE5CBB886543A03930B81DCCFE02205DEF5E400D7540BB27FBB586D`，14715 B）⇒ §P0/§P1/§P2 的 12 条针对这一版
  - **当前基线（重钉）**：归一化 SHA256 前16 = **505A19BA71BB829F**（全 64 位 `505A19BA71BB829F012C9EA526D4CD6B4C2C56345C916ABDCB63C32AB464572F`，16255 B，即作者 `2d46af3` 交付的版本）⇒ §重钉 一节针对这一版
  - 归一化 = `path.read_bytes().replace(b"\r\n", b"\n")` 之后再算 SHA256（工作区 CRLF、git 存 LF）
  - 重钉时一并核到本页配图：`figures/model-of-computation.svg` 归一化 SHA256 前16 = `9A7155CC8B390CE5`（2378 B）
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

**旧基线 `D191F6A3DCE5CBB8`**：P0（事实错误）**2 条** ｜ P1（易误解/依据不足）**5 条** ｜ P2（措辞）**5 条**（共 12 条，逐条见下）

**当前基线 `505A19BA71BB829F`（重钉）**：P0 **0 条** ｜ P1 **0 条** ｜ P2 **1 条**（12 条全部闭合；新增 1 条可选观察，见 §重钉）

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

## 重钉 · 新基线 `505A19BA71BB829F`（作者 `2d46af3` 交付，2026-09-29）

范围：**只**核作者声称改动的那 12 处（2 P0 + 5 P1 + 5 P2），并顺带核了同页被牵动的配图 `figures/model-of-computation.svg`（归一化前16 `9A7155CC8B390CE5`，2378 B）。

| 原编号 | 新版本位置 | 判定 | 依据（新版本逐字 / 回源核对） |
| --- | --- | --- | --- |
| P0-1 指针机包含方向 | L46 | ✅ 已改对 | 「换句话说，**它能做的 RAM 都能做**，反过来不成立：RAM 能表达的东西更多。」与源 p.2 `weaker than (can be implemented on) RAM` 方向一致 |
| P0-2 长文显得更远 | L81 | ✅ 已改对 | 「而这里的 \(d'\) 是距离，数大就代表远，于是结果成了「重合得越多反而显得越远」：长文档带着 99% 的重合，却比只有 10% 重合的短文档显得更远。」与源 p.5 `long documents with 99% same words seem farther than short documents with 10% same words` 一致 |
| P1-1 `algorithm` 词源 | L18 + 溯源第 7 条（L155） | ✅ 已改对（归属已标） | 正文：「顺带说一句**讲义里没有写的事**：algorithm 这个词本身就是他名字的拉丁化（经中世纪拉丁语 algorismus）」；溯源第 7 条单列 |
| P1-2 副标题三件事 | L14 | ✅ 已改对 | 「副标题是「**计算模型**、Python 的代价模型、文档距离」这三件事；讲义开头的 Lecture Overview 列的是**五条**：什么算算法与什么算时间、random access machine、pointer machine、Python 模型、以及 document distance」——与 OCW 资源页 `<title>` 及讲义 p.1 的五条 bullet 逐条一致 |
| P1-3 讲义 Figure 1 读法 | L20 + 溯源第 8 条（L156） | ✅ 已改对，并采纳了「不推断箭头」这条限制 | 「两列三行：左列自上而下是 program、programming language、computer，右列自上而下是 algorithm、pseudocode、model of computation；图例 analog 在正上方，built on top of 在最右侧。…**不替它推断连线**」——与我解出的文本坐标（program 76.7／programming language 58.7+44.3／computer 22.5；algorithm 76.5／pseudocode 52.5／model of computation 29.0+14.6；analog 101.3,98.5；built on top of 234.8–240.5,68.5–54.1）**逐项一致** |
| P1-4 `psuedopolynomial` 出处 | 溯源末段第二处登记（L158） | ✅ 已改对 | 「**OCW 日历页第 21 讲标题**里的 `psuedopolynomial` 是 OCW 原文的拼写（…本讲讲义只有 8 页，不存在第 21 页）」 |
| P1-5 溯源「第一步」 | 溯源第 5 条（L153） | ✅ 已改对 | 「讲义把**第二步里「先排序」那条路线**的代价写成 O(k log k · \|word\|)」 |
| P2-1 引文少 `bits` | L38 | ✅ 已改对 | 「讲义写的是 \(w \ge \lg(\text{memory size})\) **bits**。」 |
| P2-2 「期望 Θ(1)」未标 | L105 + 溯源第 4 条（L152） | ✅ 已改对 | 「w.h.p. 说的是「高概率成立」；至于「字典的查找与插入是期望意义下 Θ(1)」**这半句是我们的补充**，讲义两处都只写了概率式（`θ(1) time w.h.p.` 与 `O(|doc|) w.h.p.`）」——所引两式我回源核过：p.4 与 p.6 逐字一致 |
| P2-3 清单完整性 | L57 | ✅ 已改对 | 「（它另外还列了 `len(L)` 与 `L.sort()`，以及 tuple/str、dict、set、heapq、long 这几类的模型，这里只展开最常用的五项）」——与源 p.3–p.4 的 (f)(g) 与第 2–6 类逐项一致 |
| P2-4 「讲义的两张 Figure」 | 溯源（L147） | ✅ 已改对 | 「讲义的两张**编号** Figure 与若干未编号示意图一律重画，不转载」 |
| P2-5 「好几个数量级」没有出处 | L12 | ✅ 已改对 | 「耗时能差出好几个数量级（这个量级感来自讲义**第 7 页**那张实测表：228.1 秒到 0.2 秒）」——源 p.7 确实是那份实测表 |

**12/12 全部改对；重钉范围内也没有发现改动引入新的、与源冲突的断言。**

### 重钉时新增的一条 P2（可选，不影响事实）

- **溯源第 8 条那句「箭头的指向…一个字都没有替它推断」指的是讲义 Figure 1；而本页自绘的 `model-of-computation.svg` 里有两条箭头（计算模型 → 程序、计算模型 → 算法）与一句注脚「计算模型给两者定价」。** 那两条箭头的依据是**讲义文字**（p.1 `cost of algorithm = sum of operation costs`），不是源图，所以不算错；但建议在溯源第 8 条补半句「本页自绘的模型图只按讲义文字画关系（p.1），不表示源图也是这个连法」，免得读者把两者混起来。

---

**核对人声明**：本记录有两份基线 —— 旧基线前16 `D191F6A3DCE5CBB8`（§P0／§P1／§P2 的 12 条）与当前基线前16 `505A19BA71BB829F`（§重钉）。**当前结论以 §重钉 为准**；页面若再改动，结论不自动成立。本记录**不修改**任何正文、配图或 `status`——`status` 由 Lead 处理。

---

## ★ 差分补核（2026-09-29）· 针对基线 1816D3426BEA8474

**核对人**：非作者事实核对者（**差分补核**）。本讲全部写作与配图由作者 `mit6006-author` 完成，本次核对与作者无讨论；每一行判定都只引源材料。**不修改正文、配图与 `status`。**

**范围声明**：本次**不是**对新版本重跑全量；**只核作者这一轮改动的那几处**（`7b2e985` 相对上一基线 `505A19BA71BB829F` 的 diff）。
原记录（基线 `505A19BA71BB829F`）的结论**对当前版本不再自动成立**：它针对的是更早那一轮（`2d46af3`）改的 12 处，而这一轮改的是另一批位置。

- 被核对版本：`content/02-models-of-computation-document-distance/index.md`
  - **当前基线**：归一化 SHA256 前16 = **1816D3426BEA8474**（全 64 位 `1816D3426BEA8474A397A49F50C587D2F38A5CC7C2669292436D126C8EDCBE6B`，归一化 18,590 B）
  - 归一化口径同前：`read_bytes().replace(b"\r\n", b"\n")` 后算 SHA256
  - 本轮新增的图：`figures/docdist-multipliers.svg` 归一化前16 = `C44E050E71D49FBE`（3,553 B；与 `docs/audit/visual-review/mit-6.006__docdist-multipliers.md` 里记的对象指纹一致）
- **我看到的 diff（不采信 commit message，逐句读的 patch）**：改动落在 L12（D4）、L20（图例改述——**不在 D1–D4/E1–E4 清单里，我一并核了**）、L48（D2）、L54（E1）、L63（E3/E4）、L79（E2）、L91–L93 与 L109（D3）、L130–L139（D1 + 新图）、L147（D2）、L160–L176（溯源重排）。**表格 L119–L128 与其余段落未动**（因此不在本次范围内）。
- **源材料与抽取器（本次实际用的）**
  1. `_sources/MIT6_006F11_lec02.pdf`（966,809 B，SHA256 前16 `7B5596D221433C27`）。三道校验：① 体积 966,809 **不是 2 的整数次幂**；② 尾部逐字为 `startxref` / `116` / `%%EOF`；③ **现抓同一 URL 回来逐字节相同**（`curl.exe -s -L --max-time 90 --retry 3 --retry-all-errors -x socks5h://127.0.0.1:7892`，exit 0，966,809 B，同一 SHA256）⇒ 盘上这份就是 OCW 现在服务的文件。URL 取该页 front matter 的 `source_url` 所指的 OCW 讲义（`…/6b9b20992d8c6a0f3f10a34ff7878aa9_MIT6_006F11_lec02.pdf`）。
  2. **我这次用的抽取器**：`pypdfium2 5.13.0`（仓内 `_tmp_libs/`；逐页 `get_text_range()`；脚本在 `%TEMP%\cl6a\pdfx.py`，产物 `%TEMP%\cl6a\MIT6_006F11_lec02.pdfium.txt`，8 页 6,971 字符）。**本节的页码一律指 PDF 页码**（p.1–p.8）。
  3. 交叉校验（沿用仓内既有文本）：`_sources/MIT6_006F11_lec02.pdf.clean.txt`（盘上 7,691 B，CRLF→LF 归一化后 SHA256 前16 `FD0C569A261DF5DA` —— **正是上一轮记录里那个 pypdf 产物的指纹**，两者 B 数之差 7691−7438=253 就是 253 个 CRLF，内容相同）。两套抽取在**本次用到的每一条字符串上逐字一致**：8 个耗时、`words = words + words on line` 等八行注记、两篇文本规模、`Pentium 4, 2.8 GHz, C-Python 2.62, Linux 2.6.26`、`(a)`–`(g)` 编号、`weaker than (can be implemented on) RAM`、`where |Di| is the number of words in document i`。**⇒ 抽取器不影响本次任何判定。**
  4. 溯源备注（诚实记录）：上一轮记录写的 PDF 指纹是 966,515 B / `85CC80CEEB145CCB`，与现在盘上（及现抓）的 966,809 B / `7B5596D221433C27` **不是同一个字节流**（差 294 B，非换行所致）。我**复现不出**那份旧副本；但两者的文本层在本次用到的所有位置一致（见上），故不改变任何判定。

### D1 重算：我自己把 p.7 那张表的 8 个数字取出来除了一遍

| 相邻两行 | 相除 | 1 位小数 | 作者写的倍数 | 判定 |
| --- | --- | --- | --- | --- |
| docdist1→2 | 228.1 / 164.7 = 1.3849 | **1.4** | 把拼接换成 `+=` 1.4 倍 | ✅ |
| docdist4→5 | 71.7 / 18.3 = 3.9180 | **3.9** | 把拆词换成 `string.translate` 3.9 倍 | ✅ |
| docdist7→8 | 1.8 / 0.2 = 9.0000 | **9.0** | 把逐行处理换成整篇 9 倍 | ✅ |
| docdist5→6 | 18.3 / 11.5 = 1.5913 | **1.6** | 插入排序换成归并排序 1.6 倍 | ✅ |
| docdist6→7 | 11.5 / 1.8 = 6.3889 | **6.4** | 排序整个换成字典 6.4 倍 | ✅ |
| （图上多出的两根）docdist2→3 / docdist3→4 | 164.7/123.1 = 1.3379 ／ 123.1/71.7 = 1.7169 | 1.3 ／ 1.7 | 图上标 `归并式点积 1.3×` / `字典计数 1.7×` | ✅（数值与源行注 `(3)'` / `(2)'` 对得上） |
| 整段 | 228.1 / 0.2 = 1140.5 | — | 「一千多倍」 | ✅ |

**五个倍数全对，而且每一对都挂在 p.7 正确的那两行上**（不是数字碰巧对、行配错）。源 p.7 逐字：`seconds on Pentium 4, 2.8 GHz, C-Python 2.62, Linux 2.6.26` + `docdist1: 228.1` / `164.7` / `123.1` / `71.7` / `18.3` / `11.5` / `1.8` / `0.2`。（先前的 P2-5「好几个数量级」已改掉，本轮没有回头。）

### 逐处回源

| # | 作者改了什么 | 回源结果 | 判定 |
| --- | --- | --- | --- |
| **D1** | 撤掉「真正的大头不是换算法…各自都是一次量级的跳跃」，改成按表算出的两分类（动写法与常数因子 / 动数据结构）并给出五个倍数 | 五个倍数**逐行重算全部正确**，行配对也正确（见上表）；「一次量级」这句夸大已消失 | ✅ |
| **D1·归属** | 「讲义只给了数字，没有写出这两句；倍数是从它那张表算出来的」 | **确实写在页面里**（L139 逐字），且溯源第 6 条另有登记；源 p.7 只有八个耗时 + 每行一句改动，**没有**任何结论句、也没有标出任何倍数 ⇒ 归属声明成立 | ✅ |
| **D1·新加的半句** | 「而**这三步算法本身一次都没换**」 | **与源 p.7 的行注不符**：docdist3 = `(3)'`、docdist4 = `(2)'`、docdist7 = `(3) (full dictionary)` ⇒ 同一张表在**步骤 2 与步骤 3 上各换过一次实现**，而 p.6 给的是**两条复杂度不同的路线**（计数：`O(k log k ·\|word\|)` 对 `O(\|doc\|) w.h.p.`；点积：`O(k1 · k2)` 对归并指针）。本页自己的表格行也这么写（L123「点积改用归并式」、L124「计数改用字典」、L127「计数完全用字典，排序彻底去掉」）。只有按「三步的**分解**没变、变的是每步的实现」读才成立 | ❌ **P1-1** |
| **D1·新图** | 新增 `figures/docdist-multipliers.svg`（7 根柱，蓝=写法/紫=数据结构） | **数值与柱高 ✅**：7 个柱标签全部等于表里相邻两行相除（含上面五个 + 1.3 / 1.7）；柱高也自洽 —— 7 根**同一底边** `y+h = 170`，用一个比例尺就能全部对上（`round(v × 6.57)` 七根全中，`s=6.6` 时 `1.4→9、1.3→9、1.7→11、3.9→26、1.6→11、6.4→42、9.0→59` 与画出的 9/9/11/26/11/42/59 逐一相同），不存在柱子与标签反向。**但配色与正文的两分类打架**（详见 P1-2） | ❌ **P1-2** |
| **D2** | 新增「既然更弱，为什么还要留着它？…（**这一句是讲义没有写、我们补的理由**）」，并把「为什么它反而更好实现」改成「既然更弱，为什么这一讲还要留着它」 | 源 p.2 的 Pointer Machine **只有四条 bullet**：`dynamically allocated objects (namedtuple)` / `object has O(1) fields` / `field = word (e.g., int) or pointer to object/null (a.k.a. reference)` / `weaker than (can be implemented on) RAM` —— **没有**任何「为什么还留着它」的理由 ⇒ 声明正确；L48 正文、溯源第 7 条、L147 三处口径一致 | ✅ |
| **D3** | 归一化点积改号成 \(\lVert D_1\rVert\cdot\lVert D_2\rVert\)，并明说「同一个竖线在两处指的不是同一件事」 | 源 p.5 那个式子**原本用单竖线**：`d//(D1,D2) = D1 · D2 / \|D1\| · \|D2\|`，紧接着逐字 `where \|Di\| is the number of words in document i`；而 `\|doc\|` 在 p.6 两处都是**字符数**（`→ for char in doc:` 右边的 `Θ(\|doc\|)`）⇒「`\|D_i\|` 是词数、`\|doc\|` 是字符数、同一个竖线不是同一件事」**成立**；`‖·‖` 是改号，溯源第 8 条已登记 | ✅（改号这件事本身；命名问题见 P2-1） |
| **D4** | 撤掉「Python vs C 差好几个数量级」的引子，改成「那张表的八行全在同一台机、同一个 CPython 2.6.2 上跑，只改 Python 代码，就从 228.1 秒掉到 0.2 秒」 | 源 p.7 的表头**就是这么写的**：`seconds on Pentium 4, 2.8 GHz, C-Python 2.62, Linux 2.6.26`，八行同属一份实测记录、行注全是 Python 代码层面的改动（`words += words`、`with insertion sort`、`merge sort (vs. insertion)`…）⇒ 三句都成立；L117 的机器配置也与源逐字一致 | ✅ |
| **E1** | 新增「计算模型有**两个**（RAM 与指针机），Python 的代价模型是**第三个东西**，而且它不是一个新机器——它是一张对照表」 | 源 p.1 的 Lecture Overview 是**五条**（`What is an algorithm? What is time?` / Random access machine / Pointer machine / **Python model** / Document distance）；正文里 Python 一节写的是 `Python lets you use either mode of thinking` 与 `imagine implementation in terms of (1) or (2)` ⇒「两个计算模型 + Python 不是新机器」是对源的**读法**（Overview 确实把 `Python model` 与两个模型并列成第三条 bullet），而页面已把这条读法登记为补充（溯源第 7 条）⇒ **不判错** | ✅（读法已登记） |
| **E2** | 第五节不再用「第一步」，三步只属于第六节 | 源 p.5 是**先定义**（`Think of document D as a vector`、`D[w] = # occurrences of word W`、两个公式、`where \|Di\| …`、`arccos`），**再另起一节** `Document Distance Algorithm` 列 `1. split each document into words` / `2. count word frequencies (document vectors)` / `3. compute dot product (& divide)` ⇒「看成向量」留在定义节、三步留在算法节**与源的分节一致**；页内 grep `第一步` ⇒ **0 处**（`第二步` 只剩溯源第 3、5 条在说源自己的第二步，正确） | ✅ |
| **E3/E4** | 溯源「Python 的两个模型与 a 到 e 五项操作的代价」→「Python 的代价模型与五项常用操作的代价」；新增「第五条那一个圆点里含 `x in L`、`L.index`、`L.find` 三种写法，讲的是同一件事」 | 「五项」与源 (a)–(e) 逐一对应（`L.append(x)` / `L = L1 + L2` / `L1.extend(L2)` / `L2 = L1[i:j]` / `b = x in L`）；第五条确含**三种**写法（源 (e)：`b = x in L`、`& L.index(x)`、`& L.find(x)`）✅。**但**：源里那五条**有 (a)–(e) 编号**，而且一路编到 (f) `len(L)`、(g) `L.sort()` ⇒ 去掉「a 到 e」不是假话，却丢掉了一个**真实存在**的回源抓手（把五项标成 (a)–(e) 即可两全） | ✅（正文不假）＋ **P2-2** |
| **清单外的 L20** | 「图例 analog 在正上方，built on top of 在最右侧」→「两个图例是 analog（类比）与 built on top of（建立在……之上），前者在正上方，后者在最右侧」 | 源 p.1 确有这两个图例字符串（`analog`、`built on` / `top of`）；方位与上一轮用 Form XObject 坐标钉过的结论一致（analog 顶部居中、built on top of 最右）；两个括注是译名 | ✅ |

**新发现**（这一轮改动引入的）：

1. **P1-1 · 「这三步算法本身一次都没换」（L130，本轮新句）**——源 p.7 的行注 `(3)'` / `(2)'` / `(3) (full dictionary)` 说明步骤 2、3 各自被换过一次实现，p.6 还给了两条**复杂度不同**的路线；本页 L123–L124 也写着「点积改用归并式」「计数改用字典」。这正是陌生读者当初报的那类矛盾（「不是换算法」对「下面列的却是换算法」）——本轮把措辞换成更硬的「**一次都没换**」，矛盾没有闭合。建议改成「三步的**分解**没变，变的是每步的实现、数据结构与常数因子」。
2. **P1-2 · 新图 `docdist-multipliers.svg` 的配色与图例，和它自己的 desc、正文的三句话不能同时成立**——逐字摆开：
   - 正文 L132–L133 的两分类：**写法/常数因子** = {`+=` 1.4、`translate` 3.9、整篇 9}；**数据结构** = {归并排序 1.6、全字典 6.4}。
   - 图的 `<desc>`：「动写法的几步买到 **1.4 到 9** 倍，动数据结构的两步分别买到 1.6 倍与 6.4 倍」⇒ 与正文**一致**（9 倍算写法、数据结构是**两步**）。
   - 图内图例（第 39 行）：「蓝＝动写法与常数因子，紫＝动数据结构」；而实际填色是**蓝 4 根** {`+=` 1.4、归并式点积 1.3、字典计数 1.7、`translate` 3.9}、**紫 3 根** {归并排序 1.6、全字典 6.4、**整篇处理 9.0**} ⇒ **「整篇处理」被涂成数据结构色**（正文说它是写法），「字典计数」「归并式点积」被涂成写法色（前者恰恰是换字典这个数据结构改动）⇒ 同一分类在图与正文里各指一套。
   - 图注 `alt`（L137）：「动写法的几步最多 9 倍，动数据结构的**那一步** 6.4 倍」⇒ 与正文/desc 的「数据结构**两步**（1.6 与 6.4）」又不一致。
   - 另外正文与 desc 都只讲 5 个改动，图却画了 7 根柱（多出「归并式点积 1.3」「字典计数 1.7」在正文里**一处也没有**），读者没法在文字里找到这两根的出处。
   - 说明：这不是「数值错」——7 个数值与柱高我都核过，全对（见上表）；`docs/audit/visual-review/mit-6.006__docdist-multipliers.md` 判「配色与图例一致」指的是**图内**自洽（蓝4紫3确实与它自己的图例对应），它看不到正文，故不冲突。这里是**文↔图**不一致，需要作者统一一方。
3. **P2-1 · `‖D_i‖` 同时被叫「范数/向量的长度」和「词数」（L93）**——源 p.5 逐字是 `where |Di| is the number of words in document i`，即那个量**就是词数**，不是欧氏范数（欧氏范数应为 \(\sqrt{\sum_W D_i[W]^2}\)）。本轮为了消歧把记号换成 `‖·‖` 并称之为「**范数**记号」，等于给一个词数贴了标准数学记号的标签；页面自己也在同一句里定义成「词数」，读得懂，但严格读者会指认这处混用（源的公式本来就是按词数归一化、不是按欧氏范数）。建议：保留源的单竖线 `|D_i|`，或写成「\(\lVert D_i\rVert\) 在本篇指第 i 篇的词数（源用 `|D_i|`；严格说它不是欧氏范数）」。
4. **P2-2 · 溯源去掉「a 到 e」，但源里确实有 (a)–(g) 编号**——源 p.3–p.4 的五条正是 `(a)` `(b)` `(c)` `(d)` `(e)`，后面还有 `(f) len(L)` 与 `(g) L.sort()`；页内与页内配图上没有 a–e（这是陌生读者报这条的原因），但**源有**。「五项常用操作」这句话本身不假，只是与源失去了一一对应的锚点。
5. **P2-3 · 溯源第 6 条引的还是上一版的句子**——溯源写「**「大头的改动是数据结构与常数因子」**这句总结与表里每一步的倍数」，而新版正文 L139 说的是「常数因子值得改，数据结构换对了更值得改」；被引的那句已经不在页面上（它是 `2d46af3` 那版的措辞），书签没跟上。另外溯源第 8 条（把记号换成 `‖·‖`）是**记号**类改动，却被归进「后五处是关于**归属与自检**的」那一组（前五处标题写的是「量与记号」）——分组与内容错一档，不影响事实。

**仍未闭合**（若有）：

- **D1 那一类矛盾（「不是换算法」）没有完全闭合**：新句「这三步算法本身一次都没换」把同一处张力换了更硬的措辞（P1-1），而正文自己下面两条就又举了「插入排序换成归并排序」「排序整个换成字典」。
- **新图与其正文的分类没有统一**：正文两分类 / 图 desc / 图 alt / 柱色 四方各说一套（P1-2），其中柱色与正文直接相反。
- 溯源第 6 条仍是旧句书签（P2-3），读者按它去正文找不到那句话。

**我核不到的**（诚实记录，含检索词与范围）：

- **「这三步算法本身一次都没换」的作者本意是哪一种读法**（「三步的分解」还是「每一步的算法」）：源里**没有**任何一句定义「什么算换算法」，我只能按源 p.7 的行注（`(2)'`、`(3)'`、`(3) (full dictionary)`）与 p.6 的两条路线判它对不上；若作者本意是前者，此处降为措辞问题（但 P1-2 的图仍要改）。
- **上一轮记录里那份 PDF 副本**（966,515 B / `85CC80CEEB145CCB`）：现抓与盘上都是 966,809 B / `7B5596D221433C27`，我复现不出旧副本，也无法判断那份是更早的 OCW 版本还是当时抓取方式不同；文本层一致性已用两套抽取器比过（见「源材料」4），不认为会改变任何判定。
- **图里「归并式点积 1.3」到底对应哪两行**：源 p.7 **没有**把倍数标出来，我是用「相邻两行相除 + 该行注记」推出的（docdist2→3 = `(3)'`、docdist3→4 = `(2)'`），数值能对上；但这是**我的推断**，不是源的原话。
- **检索范围与词**：本讲 **8 页全部**逐页读过（两套抽取器各一遍）；关键词 `docdist`、`Pentium`、`C-Python`、`weaker than`、`number of words`、`\|D`、`(a)`–`(g)`、`w.h.p.`；中文页内 grep `第一步`（0 处）、`第二步`、`范数`、`最常用`、`a 到 e`（0 处）。在本讲内找「为什么保留指针机」的理由 ⇒ **0 命中**；找结论句或倍数 ⇒ 只在 p.7 找到八个耗时与每行一句改动，**没有**结论、**没有**倍数。
- **我不做的事（与上一轮同样的限制）**：不重跑 `audit_content.py` / `check_figures.py`，不渲染 SVG 量墨迹（那是机检与视觉复核的活）。`docdist-multipliers.svg` 的**视觉**复核另有报告（对象 SHA 前16 `C44E050E71D49FBE`，我算出的归一化值一致）；我的 P1-2 是**文↔图**核对，不否定那份报告。
- 本讲讲义之外的主张（CLRS 惯例、`psuedopolynomial`、词源等）本轮**未再核**：它们不在这一轮 diff 里，结论仍以 §重钉 为准（本节只重申「那一批改动与这一批不相交」）。

**结论（只针对这一轮改动）**：P0 **0** 条 ｜ P1 **2** 条（P1-1「三步算法一次都没换」；P1-2 新图配色/图注与正文两分类不一致）｜ P2 **3** 条（P2-1 `‖D_i‖` 的「范数」命名；P2-2 溯源去掉 a–e；P2-3 溯源第 6 条旧句书签 + 第 8 条分组）。
**数值层面：D1 的五个倍数、七个柱值、柱高比例尺全部正确**；本轮的问题集中在**分类/措辞与书签**，不在数字。
