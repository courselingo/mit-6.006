# 授权核实记录 · MIT 6.006 Introduction to Algorithms（OCW Fall 2011）

- 核实人：CourseLingo 课程作者（agent `mit6006-author`）
- 核实日期：**2026-09-28**
- 结论：**A 级（允许衍生）** —— 可做中文译文与改编，义务为 **署名 + 非商用 + 同协议（CC BY-NC-SA 4.0）**
- 落地位置：本仓库 `course.toml` 的 `[license]` 与 `[license.materials]`

## 1. 方法（沿用 docs/course-catalog.md 的既有坑）

- **抓原始 HTML**，不过滤标签后再搜文本（许可常常只是一个 JSON-LD 字段或页脚链接）。
- 走 `socks5h://127.0.0.1:7892`，失败重试；**`000` 一律重试，从不当成 404**。
- **逐页取证**：OCW 的许可是**逐页复制**的，一个页面上有徽章**推不出**别的页面也有。
  反例是 6.824：主页带 CC BY 3.0 US 徽章，而 `notes/l01.txt` 等子页面 0 命中。
- 反查假阴性：同时搜 `All rights reserved`、`excluded from`（后者是 6.828 页面上那种
  「本内容被排除在 CC 许可之外」的第三方标注）。

## 2. 逐页证据

| # | 页面 | URL | `by-nc-sa` 命中 | `All rights reserved` | `excluded from` |
| --- | --- | --- | --- | --- | --- |
| 1 | 课程页 | <https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/> | **2** | 0 | 0 |
| 2 | 讲义页 | <https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/> | **2** | 0 | 0 |
| 3 | 大纲页 | <https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/syllabus/> | **2** | 0 | 0 |
| 4 | 第 1 讲资源页 | <https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/resources/lecture-1-algorithmic-thinking-peak-finding/> | **2** | 0 | 0 |

**四页一致的逐字证据**（每页各 1 次 JSON-LD + 1 次可见页脚，所以每页恰好 2 次命中）：

```html
<!-- JSON-LD（课程页；四页同款，各 1 次） -->
"license": "https://creativecommons.org/licenses/by-nc-sa/4.0/",

<!-- 可见页脚（四页同款，各 1 次） -->
© 2001–2026 Massachusetts Institute of Technology
<a href="https://creativecommons.org/licenses/by-nc-sa/4.0/" target="_blank">Creative Commons License</a>
```

`evidence_url` 取讲义页（#2）：它是本课程实际依据的材料页，而不是只挂徽章的门面页。

## 3. 条款解释与义务

`CC BY-NC-SA 4.0` = Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International：

| 要素 | 含义 | 对我们的约束 |
| --- | --- | --- |
| **BY**（署名） | 必须署名 | 每页给出原课程名、机构、讲次与原文链接 |
| **NC**（非商用） | 不得用于商业用途 | 本站产出**不得**进入付费/会员/广告等商业场景 |
| **SA**（相同方式共享） | 衍生作品须以同一协议发布 | 我们的中文讲解若构成改编，须以 CC BY-NC-SA 4.0 发布 |
| 允许衍生 | 翻译属于衍生作品 | 所以**可以做译文**（与 B 级课程的关键区别） |

> 「一课程一仓库」的隔离设计正为此存在：本仓库的产出协议是 CC BY-NC-SA 4.0，
> 不能与 BY-SA（CS168）、BY-NC（15-442）、MIT（CSE 234）混进同一个仓库。

## 4. 逐材料类型的判定（`[license.materials]`）

**「讲义已授权」不等于「视频也已授权」**，所以按类型分别记：

| 类型 | 判定 | 依据与理由 |
| --- | --- | --- |
| `notes` | **true** | 讲义页（#2）带 CC BY-NC-SA 4.0，已逐字取证。本课程实际依据的就是讲义 PDF |
| `slides` | false | 幻灯片 PDF **本体未逐个打开**核实。页面许可块是逐页复制的，四页一致给了正面信号，但页面覆盖范围不等于文件覆盖范围 ⇒ 保守记为未核实 |
| `video` | false | 视频叠加平台条款（archive.org / YouTube），本项目**不做字幕翻译**；讲座视频不进入产出范围 |
| `textbook` | false | 指定教材是 CLRS（Pearson 商业出版物），与 OCW 许可**无关**，不能跟着课程许可走 |
| `other` | false | 未逐项核实 |

**永久排除（与授权无关，不开任何口子）**：作业与考试的题面、参考答案。
著作权与学术诚信双重风险，与 6.824 / 6.1810 / CS 144 同一处理。

## 5. 复核状态（诚实记录）

- 本记录由**作者本人**完成，属于 SOP 阶段② 要求的「实际访问 + 逐字摘录」。
- SOP 阶段② 的**人工闸门要求第二人独立复核**（双人签字）。
  截至本文件写入时，**第二人复核尚未完成** —— 未完成前不得把任何讲座的
  `output_mode` 从 `explanation` 改为 `transcript`。当前第 1 讲是 `explanation`，不受此阻塞。
- 复核方法：重新抓上表 4 个 URL 的原始 HTML，对 `by-nc-sa`、`All rights reserved`、
  `excluded from` 三个词各数一次，与上表比对。
