# 讲次清单 · MIT 6.006 Introduction to Algorithms（Fall 2011）

> 本文件定义这门课的「**全量**」= 下表 **24 个讲授单元**。逐讲产出一页。
> 授权：**CC BY-NC-SA 4.0**（OCW 是**逐页复制**的许可：课程页与每个讲义资源页各自带一次 JSON-LD 许可，
> 页脚另有可见的同一 URL 链接）。第二人复核见 `docs/audit/license-ocw-6.006-second-review.md`。
> 产出形态：`output_mode = "explanation"`（**按源讲次的结构写中文讲解**），依据
> 平台仓库 `docs/output-mode-decision.md`；译文（`transcript`）**授权已解锁但本课程选择不做**。

## 授权边界（写作时不变）

- **可用**：OCW 讲次讲义（**typed notes 为主**，即 `mit6_006f11_lecNN`）；同一讲的**手写原稿**
  （`…_orig`）只在需要核对细节时使用（它是**同一讲的另一版**，不是另一讲）。
- **配图**：**自绘 SVG，不转载原图** —— 讲义里的 Figure 1/Figure 2 一律重画（房规硬要求）。
- **引用方式**：`explanation` 形态下**只给「原文短引 + 中文」**，不复制原句成段。
- **逐页原则**：若要**把某一讲改成 `transcript`**，必须先**单独取证该讲的资源页**（下表的 URL 即取证入口）。
- **永久排除**：作业（problem sets）与测验/考试（Quiz 1、Quiz 2）的题面与解答。
- **代码包**（`lec02_code`、`lec06_code`）可作为**事实来源**（例如第 2 讲的八个版本与计时），
  但**不转载其代码**，只在正文里转述实测数字。

## 讲次表（24 讲，标题逐字取自 OCW 日历页 TOPICS 列）

| # | slug（拟定） | 标题（OCW 原文） | 材料页（署名与取证依据） |
| --- | --- | --- | --- |
| 1 | `01-algorithmic-thinking-peak-finding` | Algorithmic thinking, peak finding | `…/resources/mit6_006f11_lec01/` |
| 2 | `02-models-of-computation-document-distance` | Models of computation, Python cost model, document distance | `…/resources/mit6_006f11_lec02/`（另有 `_orig` 手写稿、`lec02_code`） |
| 3 | `03-insertion-sort-merge-sort` | Insertion sort, merge sort | `…/resources/mit6_006f11_lec03/` |
| 4 | `04-heaps-and-heap-sort` | Heaps and heap sort | `…/resources/mit6_006f11_lec04/` |
| 5 | `05-binary-search-trees-bst-sort` | Binary search trees, BST sort | `…/resources/mit6_006f11_lec05/` |
| 6 | `06-avl-trees-avl-sort` | AVL trees, AVL sort | `…/resources/mit6_006f11_lec06/`（另有 `_orig`、`lec06_code`） |
| 7 | `07-counting-radix-sort-lower-bounds` | Counting sort, radix sort, lower bounds for sorting and searching | `…/resources/mit6_006f11_lec07/`（另有 `_orig`） |
| 8 | `08-hashing-with-chaining` | Hashing with chaining | `…/resources/mit6_006f11_lec08/`（另有 `_orig`） |
| 9 | `09-table-doubling-karp-rabin` | Table doubling, Karp-Rabin | `…/resources/mit6_006f11_lec09/`（另有 `_orig`） |
| 10 | `10-open-addressing-cryptographic-hashing` | Open addressing, cryptographic hashing | `…/resources/mit6_006f11_lec10/` |
| 11 | `11-integer-arithmetic-karatsuba` | Integer arithmetic, Karatsuba multiplication | `…/resources/mit6_006f11_lec11/` |
| 12 | `12-square-roots-newtons-method` | Square roots, Newton's method | `…/resources/mit6_006f11_lec12/` |
| 13 | `13-breadth-first-search` | Breadth-first search (BFS) | `…/resources/mit6_006f11_lec13/`（另有 `_orig`） |
| 14 | `14-depth-first-search-topological-sort` | Depth-first search (DFS), topological sorting | `…/resources/mit6_006f11_lec14/`（另有 `_orig`） |
| 15 | `15-single-source-shortest-paths` | Single-source shortest paths problem | `…/resources/mit6_006f11_lec15/` |
| 16 | `16-dijkstra` | Dijkstra | `…/resources/mit6_006f11_lec16/` |
| 17 | `17-bellman-ford` | Bellman-Ford | `…/resources/mit6_006f11_lec17/` |
| 18 | `18-speeding-up-dijkstra` | Speeding up Dijkstra | `…/resources/mit6_006f11_lec18/` |
| 19 | `19-memoization-subproblems-fibonacci-shortest-paths` | Memoization, subproblems, guessing, bottom-up; Fibonacci, shortest paths | `…/resources/mit6_006f11_lec19/`（另有 `_orig`） |
| 20 | `20-parent-pointers-text-justification-blackjack` | Parent pointers; text justification, perfect-information blackjack | `…/resources/mit6_006f11_lec20/`（另有 `_orig`） |
| 21 | `21-string-subproblems-edit-distance-knapsack` | String subproblems, psuedopolynomial time; parenthesization, edit distance, knapsack | `…/resources/mit6_006f11_lec21/`（另有 `_orig`） |
| 22 | `22-two-kinds-of-guessing-piano-tetris` | Two kinds of guessing; piano/guitar fingering, Tetris training, Super Mario Bros. | `…/resources/mit6_006f11_lec22/`（另有 `_orig`） |
| 23 | `23-computational-complexity` | Computational complexity | `…/resources/mit6_006f11_lec23/`（另有 `_orig`） |
| 24 | `24-algorithms-research-topics` | Algorithms research topics | `…/resources/mit6_006f11_lec24/`（另有 `_orig`，覆盖后半程） |

> URL 前缀统一为
> `https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011`，
> 表内用 `…` 省略。**每讲的 `source_url` 必须写完整 URL**（front matter 里不能省略）。

**⇒ 24 个讲授单元。**

## 不计入的项与理由

| 项 | 为什么不计入 |
| --- | --- |
| **Quiz 1**（Unit 3 之后）、**Quiz 2**（Unit 6 之后） | 是**测验**不是讲次：日历页的 LEC # 列为空、没有 TOPICS 列内容，也没有对应讲义 |
| **Problem sets 1–7** | 作业题面与解答：本项目**永久排除**（授权边界） |
| **Recitation（习题课）** | 2011 版 OCW 的讲义页与日历页里**都没有** recitation 条目；若将来发现另行开一档 |
| 讲义页上的 `lec02_code` / `lec06_code`（ZIP） | 是**代码材料**不是讲次；第 2 讲把它当**实测数字的来源**引用（8 个版本与计时），不转载代码 |
| `…_orig` 手写稿 | 是**同一讲**的另一版讲义，不单独成页（第 2/6/7/8/9/13/14/19–24 讲有） |

## 备注（数据来源与自查）

- 讲次清单取自 OCW 的 **`/pages/lecture-notes/`**（资源链接）与 **`/pages/calendar/`**（LEC # 与 TOPICS），
  两份页面都已下载到本地并解析：
  - 日历页表格共 **35 行** = 表头 1 + Unit 分组 8 + 讲次 24 + Quiz 2 ⇒ **讲次 24** ✓（**行数与讲次数对得上**，不是估的）。
  - 讲义页解析出 **39 个** `/resources/…` 链接，按 `lecNN` 归并后 **24 讲全覆盖** ✓。
- **标题逐字**取自日历页 TOPICS 列（含原文拼写，例如第 21 讲的 `psuedopolynomial` 保持原样，
  正文里再用正确拼写并说明）。
- **Unit 划分**（8 个）：Introduction / Sorting and Trees / Hashing / Numerics / Graphs /
  Shortest Paths / Dynamic Programming / Advanced Topics —— 与第 1 讲页里写的「全课 8 个模块」一致 ✓。
- 开工前逐条核对材料页可访问（`000 ≠ 404`）：第 1、2 讲已实测可取；其余各讲**产出该讲时逐讲核**。
