# Vaporware Detector 反画饼检测器

[![skills.sh](https://skills.sh/b/yangben2019/vaporware-detector)](https://skills.sh/yangben2019/vaporware-detector)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**What does this document actually say?**

A Claude Code skill that scans a business plan, funding deck, product proposal, or requirements doc for vapor — buzzwords, unsourced claims, vanity metrics, undefined core terms, and missing failure cases — then gives a credibility score and a concrete rewrite.

Not a roast. A translation layer: every sentence that cannot be checked gets flagged, and every flagged sentence gets a rewrite that could be checked.

---

## What it detects

| Detector | Example |
|---|---|
| **Buzzword density** | 「打造全链路闭环生态」/ "seamless, world-class, end-to-end solution" |
| **Unattributed claims** | 「市场反响热烈」 — how many people, when, saying what? |
| **Vanity metrics** | 注册用户数 instead of 次周留存；downloads instead of DAU |
| **Undefined terms** | 「核心竞争力是算法」 — which algorithm, and why can't others copy it? |
| **Missing negative space** | No risks, no failure conditions, no "we stop if X is false" |

Scored 0–100 across five dimensions.

---

## Install

### Option 1 — skills CLI

```bash
npx skills add yangben2019/vaporware-detector
```

### Option 2 — Claude Code plugin marketplace

```text
/plugin marketplace add yangben2019/vaporware-detector
/plugin install vaporware-detector@vaporware-detector
```

### Option 3 — manual

```bash
git clone https://github.com/yangben2019/vaporware-detector.git /tmp/vd
cp -r /tmp/vd/skills/vaporware-detector ~/.claude/skills/
```

---

## Usage

```text
帮我看看这份融资 PPT 到底说了什么，有没有画饼。
```

```text
Is this proposal real? Audit it for hype before I sign off.
```

```text
这份需求文档里哪些论断是没法验证的？
```

The skill quotes the original text for every finding — it will not paraphrase your document, because paraphrase reads as misrepresentation.

---

## Design notes

- **Quote, don't summarize.** Every finding cites the source sentence verbatim.
- **Separate "vague" from "wrong."** Most problems are unclear claims, not lies. The wording targets unverifiability, never accuses the author of deception.
- **Rewrites must be checkable.** "Add more data" is not a rewrite; "X dropped from 4h to 1.5h (internal, 2026 Q2)" is.
- **No industry judgment.** The skill evaluates whether the *argument* holds, not whether the *business* will work.
- **Short documents get no total score.** Under one page, there is not enough to score fairly.

---

## License

MIT © 2026 yangben2019
