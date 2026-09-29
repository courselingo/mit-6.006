# 质量审核记录 · 02-models-of-computation-document-distance（第 2 讲）

> §9 要求：`status = "reviewed"` 的前置条件是「**P0/P1 清零 + 有审核记录**」。
> 本文件就是那份记录。审核人：CourseLingo Lead（非本讲作者）。

## 1. 被审核版本

| 项 | 值 |
| --- | --- |
| 页面 | `content/02-models-of-computation-document-distance/index.md` |
| 归一化哈希（CRLF→LF 后 SHA256 前 16） | 见 §6（每次修复后重钉） |
| 讲次 | 第 2 讲 · 计算模型与文档距离 |
| 源材料 | MIT 6.006 Spring 2020 · Lecture 2（OCW） |
| 产出形态 | `output_mode = "explanation"`（依 `courselingo/docs/output-mode-decision.md` §3） |
| 授权 | CC BY-NC-SA 4.0（MIT OCW）。第二人复核见 `docs/audit/license-ocw-6.006-second-review.md` |

## 2. 五道机检（Lead 自己跑，不采信作者的 exit code）

| 闸门 | 退出码 |
| --- | --- |
| `validate.py --root .` | 见 §6 |
| `check_style.py --root .` | 见 §6 |
| `audit_content.py --root . --strict` | 见 §6 |
| `check_figures.py --root . --strict` | 见 §6 |
| `build_site.py --root . --out site-mkdocs` | 见 §6 |

## 3. 第一道人工闸门 · 非作者事实核对

- 记录：`docs/audit/02-models-of-computation-document-distance-factcheck.md`
- 核对人：`fig-pruner`（**非本讲作者**）
- **旧基线 P0 2 ｜ P1 5 ｜ P2 5（共 12 条）→ 重钉后 P0 0 ｜ P1 0 ｜ P2 1**

**★ 两条 P0 都是「读得很顺、方向却反了」的那一类**（`附录二十`）：
```
① 正文「RAM 能做的它都能做」 ←→ 源 `weaker than (can be implemented on) RAM`
   ⇒ **包含方向相反** ⇒ 已改为「它能做的 RAM 都能做」
② 正文「长文更像」 ←→ 源 `long documents with 99% same words seem farther…`
   ⇒ **方向相反** ⇒ 已改为「重合得越多反而显得更远」
```
**★ 作者 `2d46af3` 按记录 12 条全改；核对者逐条复核 **12/12 改对**，并钉到新基线。**

**★ 而这份记录里的两条方法学收获（本会话后来立成了判据）：**
- **「否定性结论要写清检索词覆盖了哪些写法」** —— 源写 `~4K LOC`，按 `4000`/`4,000` 都搜不到，换 `4K` 才命中
  ⇒ 立为 `附录二十一`（异写的数字）。
- **「改了结论 ≠ 重新取了证」** ⇒ 立为 `附录十九`。

## 4. 第二道人工闸门 · 配图视觉复核

- 报告：`docs/audit/visual-review/mit-6.006__*.md`（本讲 **7 张**）
- **最终：7/7 通过**（6 张「可用」+ 1 张经**实测裁定**覆盖为可用）

**★ 而那张经裁定的图值得单记（`pointer-machine`）—— 它是一次**参照物用错**：**

```
复核者原话：「中间两条箭头未与注释所称的字段行精确水平对齐。朝左的上箭头
             垂直中心比两框的 prev 行文字中心偏高约**半字高**……朝右的下箭头
             也比 next 行文字中心偏高约**四分之一字高**。」

实测（读 SVG 属性原文）：
  三行基线 y = 86 / 104 / 122      （行距 18 = fs12 × 1.5 ✓）
  文字**视觉中心** = 基线 − fs × 0.35 = **99.8** / **117.8**
  两条箭头        y = **100** / **118**           （`M372,100 L 363,100`、`M357,118 L 366,118`）
  ⇒ **偏移 0.2px / 0.2px** ⇒ **对齐**
```
**⇒ 复核者量的是「箭头 vs **基线**」，而箭头对的是「**文字中心**」。**
**⇒ 而同一张图它给了两个**互不一致**的估计（6px 与 3px），真实偏移是**均匀的 4px = 0.2px 中心偏移**。**
**⇒ 裁定：可用。依据与报告哈希已登记进 `docs/audit/visual-adjudications.md`（针对报告 `50643DEF0945911E`）。**

**★★ 这是本项目 `附录十一`（文字类可信、几何类必须实测）的又一个干净实例，
而且是**同一个坑的第 N 次**：几何主张量错了**参照物**（此前还有「用整框做参照」「用拼版坐标做参照」两次）。**

## 5. 第三道人工闸门 · 透镜 3（陌生读者测试）

见 §5.5。

## 6. 待填（提级前由 Lead 跑完并钉死）

```
五道机检 exit：validate=? style=? audit=? figures=? build=?
页面归一化哈希：?
透镜 3：✅ ? 题 ｜ ⚠️ ? 题 ｜ ❌ ? 题
```

## 7. 本轮修复引入了什么新错

**待填。**

## 8. 结论

**待填（等 §6 齐备）。**
