---
name: vaporware-detector
description: Scan a business plan, product proposal, funding deck, requirements document, or any impressive-sounding text for vapor — buzzwords, unsourced adjectives, vanity metrics, undefined core terms, and missing failure cases — then give a credibility score and a concrete rewrite. Use when the user wants to check whether a plan is real, asks if a proposal is full of hot air, wants a hype audit before signing off, or says a document "sounds impressive but says nothing".
---

# Vaporware Detector 反画饼检测器

输入一份看起来很厉害的文件，输出它到底说了什么。目标不是嘲讽作者，是**把不可证伪的话变成可验证的话**。

The output is not a roast. It is a translation layer: every sentence that cannot be checked gets flagged, and every flagged sentence gets a rewrite that could be checked.

## 语言 Language

用用户提问的语言写报告。**引用的原文一律保持原样**，不翻译——概括会被当成误读。改写建议跟随文件的原始语言：审中文文档就给中文改写，审英文文档就给英文改写。

Write the report in the user's language. Quote source text verbatim, never translated — a paraphrase reads as misrepresentation. Suggested rewrites follow the document's own language.

## 五个检测器

按顺序跑。每个都要引用原文，不要概括。

### 1. 空话密度 Buzzword density

中文常见空话：赋能、闭环、抓手、生态、护城河、降本增效、全链路、数字化、智能化、精细化运营、打通、沉淀、复利、飞轮

English: leverage, synergy, seamless, robust, world-class, best-in-class, next-generation, disruptive, holistic, end-to-end

报告：**每千字出现几个**。超过 5 个/千字，这份文件的实质性内容大概率不足。

### 2. 无主论断 Unattributed claims

没有任何来源、也没有数字的形容和因果。

- 「市场反响热烈」—— 多少人在什么时候说了什么？
- 「显著提升效率」—— 提升多少？和什么比？
- 「用户普遍认为」—— 谁的调查？样本多大？

报告：逐条列出，标注**缺的是数字、来源，还是定义**。

### 3. 伪指标 Vanity metrics

看着很大，但和成败无关的数字。

| 伪指标 | 为什么不算数 | 该换成什么 |
|---|---|---|
| 注册用户数 | 不等于活跃 | 次周留存率 |
| 下载量 | 不等于使用 | 日活 / 周活 |
| 累计交易额 GMV | 不等于赚到钱 | 毛利率、净利率 |
| 覆盖城市数 | 不等于密度 | 单城市渗透率 |
| 合作方数量 | 不等于合作深度 | 有实际收入的分成 |

### 4. 未定义的核心词 Undefined terms

文件反复用、但从未定义的词。通常是这些词在承担论证，而它们没有内容。

例：「我们的核心竞争力是**算法**」—— 什么算法？为什么别人不能复制？

### 5. 反面缺失 Missing negative space

一份可信的方案一定包含**它可能怎么失败**。

检查有没有：
- 明确的风险与应对
- 什么条件下这个方案不成立
- 竞争对手为什么做不成（而不只是「他们没做」）
- 一个「如果 X 不成立，我们就停」的判定条件

**没有反面内容的方案，可信度一律打折。**

## 打分

五项各 20 分，满分 100。

| 维度 | 扣分方式 |
|---|---|
| 空话密度 | >5/千字，每超 1 个扣 4 分 |
| 无主论断 | 每处扣 3 分（上限 20） |
| 伪指标 | 每个扣 5 分（上限 20） |
| 未定义核心词 | 每个扣 4 分（上限 20） |
| 反面缺失 | 无风险章节扣 20；有但空洞扣 10 |

**评分解读**
- 80+：可以用，仍有需要补的证据
- 60–79：骨架在，但关键论断悬空
- 40–59：主要是愿景，需要重写
- <40：目前无法据此做任何决策

## 输出格式

```markdown
# 反画饼报告：<文件名>

**可信度：** 62 / 100 · <一句话结论>

## 空话清单
| 原文 | 类型 | 问题 |
|---|---|---|
| "打造全链路闭环生态" | 空话 | 三个词都是空话叠加，无法验证 |

## 无主论断
| 原文 | 缺什么 | 改写建议 |
|---|---|---|
| "效率提升显著" | 数字、基线 | "把 X 从 4 小时降到 1.5 小时（2026 Q2 内部数据）" |

## 伪指标
...

## 未定义的核心词
...

## 缺失的反面
...

## 如果只改三处
1. <最影响可信度的一处>
2. ...
3. ...
```

## 规则

- **必须引用原文。** 概括会被当成误读，原文不会。
- **区分「空」和「错」。** 大部分问题不是撒谎，是没说清楚。措辞要针对「不可验证」，不要暗示对方在骗人。
- **改写要真的可验证。** 「增加数据支撑」不算改写；给一个具体指标和量级才算。
- **不做行业判断。** 你不知道这个市场，所以只评「论证是否成立」，不评「生意是否可行」。
- 如果文件本身很短（一页以内），说明样本不足，给检测结果但不要给总分。
