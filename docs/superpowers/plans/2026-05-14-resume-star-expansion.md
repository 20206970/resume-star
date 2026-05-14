# Resume-Star-Skill Expansion Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Expand the resume-star Claude Code Skill with 7 modules across two directions — deepening resume capabilities (A) and extending into interview preparation (B).

**Architecture:** Each module adds content to the existing `resume-star/` skill directory — either modifying existing Markdown reference files or creating new ones. SKILL.md gains new flow branches for each module. All modules share the same conversational interaction pattern: user triggers → Skill processes → results shown for confirmation.

**Tech Stack:** Markdown (Claude Code Skill). No code, no tests, no build system. Validation is manual: trigger the skill in Claude Code with real inputs.

---

## File Structure

```
resume-star/
├── SKILL.md              # [MODIFY] Add new flow branches for all modules
├── jd-analysis.md        # [MODIFY] Add English keyword tables (A2)
├── project-scan.md       # [UNCHANGED]
├── star-examples.md      # [MODIFY] Add English examples (A2), batch format (A1)
├── interview-prep.md     # [CREATE] B2: interview question prediction reference
└── interview-sim.md      # [CREATE] B1+B3: mock interview + oral training reference
```

**Decomposition rationale:**
- New reference files (interview-prep.md, interview-sim.md) are independently writable — enables parallel development
- SKILL.md changes are additive (new flow branches), not restructuring — low conflict risk
- Each module's changes to SKILL.md are in separate sections, so sequential modification is safe

---

### Task 1: Add English keyword tables to jd-analysis.md (A2 — P0)

**Files:**
- Modify: `resume-star/jd-analysis.md`

- [ ] **Step 1: Append English skill categories section**

Add the following content at the end of `resume-star/jd-analysis.md` (after the existing Example section):

```markdown

## English JD Keywords

### Hard Skills (English JD)
- **Languages:** Java, Python, Go, C++, JavaScript, TypeScript, Rust, C#, Kotlin, Ruby, Swift
- **Frameworks:** Spring Boot, React, Angular, Vue, Django, Flask, Express, Next.js, Flutter, Rails
- **Tools/Platforms:** Docker, Kubernetes, AWS, GCP, Azure, MySQL, PostgreSQL, Redis, MongoDB, Kafka, RabbitMQ, Elasticsearch, Git, CI/CD, Jenkins, Terraform
- **Domains:** machine learning, distributed systems, microservices, data pipeline, NLP, computer vision, DevOps, SRE

### Soft Skills (English JD)
- Collaboration: "work across teams", "cross-functional", "collaborate with"
- Problem-solving: "troubleshoot", "debug production issues", "optimize performance"
- Learning: "fast learner", "quick to pick up", "stay current with"
- Communication: "communicate to non-technical stakeholders", "write technical documentation", "present findings"

### Implicit Requirements (English JD)
- High pressure: "thrive in a fast-paced environment", "wear multiple hats", "startup culture"
- Independence: "own end-to-end", "self-starter", "take ownership from 0 to 1"
- Full-stack: mentions both frontend and backend, mentions DevOps or infrastructure

### Weight Indicators (English JD)
- **Must-have:** "required", "must have", "proficient in", "strong experience with", listed in "Requirements" section
- **Nice-to-have:** "preferred", "bonus", "nice to have", "familiarity with", "experience with X is a plus"

## Example: Parsed English JD

**输入 (English JD excerpt):**
> Requirements: 1. Strong proficiency in Python and JavaScript/TypeScript 2. Experience with React and modern frontend frameworks 3. Familiarity with SQL databases (PostgreSQL preferred) 4. Experience with cloud services (AWS or GCP) is a plus 5. Excellent communication skills and ability to work in a cross-functional team

**输出:**
- Must-have: Python, JavaScript/TypeScript, React, SQL (PostgreSQL)
- Nice-to-have: AWS, GCP
- 隐性信号: "cross-functional team" → 需要展示跨团队协作能力；"AWS or GCP is a plus" → 公司在云化
```

- [ ] **Step 2: Verify file is valid Markdown**

Run: `head -3 resume-star/jd-analysis.md && echo "---" && tail -5 resume-star/jd-analysis.md`
Expected: First lines show existing header, last lines show the new English example

---

### Task 2: Add English examples to star-examples.md (A2 — P0)

**Files:**
- Modify: `resume-star/star-examples.md`

- [ ] **Step 1: Append English examples and output format section**

Add the following content at the end of `resume-star/star-examples.md` (after the existing Output Format section):

```markdown

## English Bullet Point Rules

English Bullet Points follow the same structure as Chinese ones:

1. **Start with a strong verb:** "Designed and implemented", "Developed", "Built", "Optimized", "Architected"
2. **Avoid weak openers:** Do not use "Participated in", "Responsible for", "Helped with"
3. **Structure:** Verb + What + How + Result/Impact
4. **Length:** 1-3 lines, information-dense, do not sacrifice technical detail for brevity

## Good English Examples

### Example 5: Course Project — Chat Application (English)

**Resume Bullet Point (copy-ready):**
> Designed and implemented a real-time chat application using WebSocket and React, supporting group messaging, typing indicators, and message persistence with PostgreSQL, handling 100+ concurrent connections in load testing

**STAR Breakdown:**
- **Situation:** Needed a real-time communication platform for a distributed systems course project
- **Task:** Designed the backend messaging architecture and implemented the WebSocket communication layer
- **Action:** Built a WebSocket server with connection pooling and message queue buffering, implemented room-based message routing with PostgreSQL for persistence, and used React for the frontend with real-time state updates
- **Result:** Successfully supported 100+ concurrent connections in load testing with sub-200ms message delivery latency

---

### Example 6: Internship — Data Pipeline Optimization (English)

**Resume Bullet Point (copy-ready):**
> Optimized ETL data pipeline processing time by 60% by redesigning the batch ingestion logic with Apache Spark, reducing daily processing window from 8 hours to 3 hours for 50GB+ datasets

**STAR Breakdown:**
- **Situation:** Company's daily data pipeline was taking 8+ hours to process, delaying downstream analytics reports
- **Task:** Identify bottlenecks and optimize the ingestion pipeline during summer internship
- **Action:** Profiled the pipeline to find I/O-bound stages, redesigned batch ingestion using Spark DataFrame operations with partition pruning and predicate pushdown, replaced row-by-row inserts with bulk operations
- **Result:** Reduced processing time from 8 hours to 3 hours (60% improvement), enabling same-day analytics for downstream teams

---

## English Output Format

When outputting in English, use this format:

```markdown
## Resume Bullet Points — Copy-Ready

1. [Strong verb] [what you did], [how/technical approach], [result/impact with metrics]
2. [Strong verb] [what you did], [how/technical approach], [result/impact with metrics]
3. [Strong verb] [what you did], [how/technical approach], [result/impact with metrics]

---

## STAR Breakdown (Interview Prep)

### 1. [Highlight keyword]
- **Situation:** [Project context and challenge]
- **Task:** [Your specific responsibility]
- **Action:** [What you did and technologies used]
- **Result:** [Quantified result or qualitative outcome]

### 2. [Highlight keyword]
- ...
```
```

- [ ] **Step 2: Verify file is valid Markdown**

Run: `grep -c "English Bullet Point Rules" resume-star/star-examples.md`
Expected: 1

---

### Task 3: Add language detection and English flow to SKILL.md (A2 — P0)

**Depends on:** Task 1, Task 2

**Files:**
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add language detection rule**

In `resume-star/SKILL.md`, find the `## 语言要求` section (near the end). Replace it with:

```markdown
## 语言检测与输出规则

### 语言检测
- JD 解析阶段自动检测 JD 语言（中文/英文）
- 如果 JD 是英文 → 所有输出（岗位画像、Bullet Point、STAR 展开）使用英文
- 如果 JD 是中文 → 所有输出使用中文
- 用户可随时用"用英文输出"/"用中文输出"强制切换语言

### 输出语言要求
- 中文输出: 统一中文，仅技术专有名词保留英文（如 Spring Boot、React、Redis）
- 英文输出: 全英文，包括岗位画像、Bullet Point 和 STAR 展开
- 不出现中英文混合的标题或描述（技术名词除外）
```

- [ ] **Step 2: Verify SKILL.md is valid**

Run: `grep -c "语言检测" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 3: Commit A2 (English support)**

```bash
git add resume-star/jd-analysis.md resume-star/star-examples.md resume-star/SKILL.md
git commit -m "feat(A2): add English JD support — keyword tables, examples, language detection"
```

---

### Task 4: Add resume review flow to SKILL.md (A3 — P1)

**Files:**
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add resume review trigger to "When to Use" section**

In SKILL.md, find the `## When to Use` section. Add these two items to the bullet list:

```markdown
- 用户说"帮我看看简历""审查简历""简历有什么问题"
- 用户粘贴了整份简历，想知道哪里该改
```

- [ ] **Step 2: Add resume review flow section**

In SKILL.md, find the line `## 量化规则`. Insert the following new section BEFORE it:

```markdown
## Resume Review (简历审查)

独立流程，不经过三阶段。当用户触发简历审查时执行。

### 触发条件
- 用户说"帮我看看简历""审查简历""简历有什么问题"
- 用户粘贴了整份简历文本

### 输入
- 用户的整份简历文本
- 目标 JD 文本（可选，如果提供则增加匹配度评估）

### 处理
1. 分析简历结构（教育背景、项目经历、技能列表、实习经历等是否齐全）
2. 如果提供了 JD → 评估 JD 匹配度（must-have 覆盖率）
3. 识别弱点：空泛描述、弱动词、缺少量化数据、格式不一致
4. 对每个问题给出具体修改建议（原文 → 建议修改）

### 输出格式

```
## 简历审查报告

### 整体评分: [高/中/低]

### JD 匹配度（如果提供了 JD）
- Must-have 覆盖: [X/Y]
- 未覆盖的技能: [...]

### 结构检查
- [✓/✗] 教育背景: [评价]
- [✓/✗] 项目经历: [评价]
- [✓/✗] 技能列表: [评价]
- [✓/✗] 实习/工作经历: [评价]

### 具体修改建议
- **第 X 段:** [原文片段] → [建议修改]（理由: [为什么]）
- **第 Y 段:** [原文片段] → [建议修改]（理由: [为什么]）

### 缺失内容
- [JD 要求但简历中未体现的技能/经历]
- [建议补充的内容]
```

### 向用户展示
> "我审查了你的简历，整体质量 [高/中/低]。主要问题是 A、B。具体修改建议如下..."

```

- [ ] **Step 3: Verify SKILL.md structure**

Run: `grep -c "Resume Review" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 4: Commit A3**

```bash
git add resume-star/SKILL.md
git commit -m "feat(A3): add resume review flow — structure check, JD matching, specific suggestions"
```

---

### Task 5: Add batch output format to star-examples.md (A1 — P2)

**Files:**
- Modify: `resume-star/star-examples.md`

- [ ] **Step 1: Append batch output format section**

Add the following at the end of `resume-star/star-examples.md`:

```markdown

## Batch Output Format (多 JD 批量处理)

当用户一次提供多个 JD 时，输出一份对照表:

```markdown
## JD 批量匹配结果

### JD 1: [公司名] [岗位名]
**匹配度:** [高/中/低] ([X/Y] must-have 命中)
**推荐亮点:** [亮点B], [亮点C]
**Bullet Point:**
> [针对此 JD 定制的分点描述]

**最缺技能:** [项目中未体现的 must-have 技能]

---

### JD 2: [公司名] [岗位名]
**匹配度:** [高/中/低] ([X/Y] must-have 命中)
**推荐亮点:** [亮点A], [亮点D]
**Bullet Point:**
> [针对此 JD 定制的分点描述]

**最缺技能:** [项目中未体现的 must-have 技能]

---

## 项目排序建议（基于所有 JD 的综合匹配）

| 排序 | 项目 | 综合匹配度 | 最匹配的 JD |
|------|------|-----------|------------|
| 1 | 项目A | 高 | JD1, JD3 |
| 2 | 项目C | 中 | JD2 |
| 3 | 项目B | 低 | — |

建议简历中优先写项目A和项目C。
```
```

- [ ] **Step 2: Verify**

Run: `grep -c "Batch Output Format" resume-star/star-examples.md`
Expected: 1

---

### Task 6: Add batch mode and project ranking to SKILL.md (A1+A4 — P2+P4)

**Depends on:** Task 5

**Files:**
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add batch mode triggers to "When to Use"**

In SKILL.md, find the `## When to Use` section. Add these items:

```markdown
- 用户粘贴了多条 JD，或说"我有多个岗位要投"
- 用户有多个项目，想知道简历里应该放哪个
```

- [ ] **Step 2: Add batch mode flow section**

In SKILL.md, find the `## Resume Review` section. Insert the following BEFORE `## Resume Review`:

```markdown
## Batch Mode (多 JD 批量处理)

当用户提供多个 JD 时自动进入批量模式。

### 触发条件
- 用户粘贴了多条 JD（用 `---` 分隔，或一次提供多个 JD 文本块）
- 用户说"我有多个岗位""帮我匹配多个 JD"

### 流程
1. **JD 批量解析:** 逐个解析每条 JD，提取各自的岗位画像
2. **项目扫描（一次）:** 扫描项目一次，结果复用给所有 JD
3. **交叉匹配:** 每条 JD 的 must-have 与项目亮点做匹配
4. **输出对照表:** 每条 JD 对应的推荐亮点 + 定制 Bullet Point + 匹配度

### 向用户展示
> "你提供了 [N] 个 JD。我分别分析了每个岗位的要求，并与你的项目做了匹配。匹配度最高的是 [JD X]，最需要补充的是 [JD Y]。"

### 项目排序建议（自动包含）
如果用户提供了多个项目:
- 基于所有 JD 的 must-have 综合统计，对每个项目打分
- 输出排序表 + 建议理由
- 格式参考 `star-examples.md` 的 Batch Output Format 部分

```

- [ ] **Step 3: Verify SKILL.md**

Run: `grep -c "Batch Mode" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 4: Commit A1+A4**

```bash
git add resume-star/star-examples.md resume-star/SKILL.md
git commit -m "feat(A1+A4): add batch JD processing with project ranking suggestion"
```

---

### Task 7: Create interview-prep.md (B2 — P3)

**Files:**
- Create: `resume-star/interview-prep.md`

- [ ] **Step 1: Write interview-prep.md**

Create `resume-star/interview-prep.md` with the following content:

```markdown
# Interview Prep Reference

## Question Prediction Rules

### 基于 JD 要求生成问题

对每个 must-have 技能，生成 2-3 个面试问题，按难度分层:

| 难度 | 特征 | 示例 |
|------|------|------|
| 基础 | 概念解释、定义、原理 | "HashMap 的底层实现是什么？" |
| 中等 | 应用场景、对比选择、优化 | "什么时候用 HashMap vs TreeMap？" |
| 深入 | 源码级理解、边界情况、设计权衡 | "HashMap 扩容时会发生什么？线程安全吗？" |

### 基于项目技术栈生成问题

从项目扫描结果中提取技术栈，对每个技术生成项目相关的追问:

- "你项目中 [技术] 用在什么场景？为什么选它？"
- "如果不用 [技术]，你会用什么替代？对比过吗？"
- "[技术] 在你项目中遇到过什么坑？怎么解决的？"

### 优先级排序

1. **JD 高频 + 项目实际使用** → 必须准备
2. **JD 高频 + 项目未使用** → 需要额外学习
3. **JD 未提 + 项目实际使用** → 可能被顺带问到
4. **通用软技能问题** → 每次面试都会问

### 通用软技能问题（每次必问）

- 自我介绍（1 分钟版 + 3 分钟版）
- 最有成就感的项目是什么？为什么？
- 遇到最大的技术挑战是什么？怎么解决的？
- 团队合作中遇到过分歧吗？怎么处理的？
- 你的优点和缺点分别是什么？

## Output Format

```markdown
## 面试预测题单

### 基于 JD 要求

#### [技能1: 技能名] — 重要度: 高
- [基础] 具体问题
- [中等] 具体问题
- [深入] 具体问题

#### [技能2: 技能名] — 重要度: 高
- [基础] 具体问题
- [中等] 具体问题

### 基于你的项目

#### [技术A: 项目中使用的技术]
- 具体问题（项目相关）
- 具体问题（项目相关）

### 通用问题
- [软技能问题列表]

### 复习优先级
1. [技能1]（JD 高频 + 项目实际使用）→ 必须准备
2. [技能2]（JD 高频 + 项目未使用）→ 需要额外学习
3. [技术A]（项目实际使用但 JD 未要求）→ 可能被顺带问到
```

## Example: Predicted Questions

**输入 JD 片段:** "熟悉 Java，了解 Spring Boot，熟悉 MySQL，有 SQL 调优经验优先"
**项目技术栈:** Java, Spring Boot, MyBatis, MySQL, Redis

**输出:**

#### Java — 重要度: 高
- [基础] Java 的垃圾回收机制了解吗？说说常见的 GC 算法。
- [中等] HashMap 的底层实现原理？Java 8 做了什么优化？
- [深入] 多线程环境下如何保证线程安全？synchronized 和 Lock 有什么区别？

#### Spring Boot — 重要度: 高
- [基础] Spring Boot 的自动配置原理是什么？
- [中等] @Transactional 注解在什么情况下会失效？

#### MySQL — 重要度: 高
- [基础] 事务的 ACID 特性是什么？
- [中等] 索引的底层数据结构？什么情况下索引会失效？
- [深入] 如何做 SQL 调优？EXPLAIN 的结果怎么看？

#### Redis — 重要度: 中（项目实际使用）
- 你项目中 Redis 用在什么场景？为什么选 Redis 而不是本地缓存？
- Redis 的持久化机制了解吗？RDB 和 AOF 的区别？

#### 复习优先级
1. Java 基础 + 集合框架（JD 高频 + 项目实际使用）
2. MySQL 索引和事务（JD 高频，尤其 SQL 调优）
3. Spring Boot 自动配置和事务（JD 要求 + 项目使用）
4. Redis 基础（项目实际使用但 JD 未明确要求）
```

- [ ] **Step 2: Verify file exists**

Run: `head -3 resume-star/interview-prep.md`
Expected: Shows "# Interview Prep Reference"

---

### Task 8: Add interview prediction flow to SKILL.md (B2 — P3)

**Depends on:** Task 7

**Files:**
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add interview prep triggers to "When to Use"**

In SKILL.md, find the `## When to Use` section. Add:

```markdown
- 用户说"面试会问什么""帮我准备面试题""技术问题预测"
```

- [ ] **Step 2: Add interview prep flow section**

In SKILL.md, find the `## Batch Mode` section. Insert the following AFTER the Batch Mode section (before Resume Review):

```markdown
## Interview Prep (面试问题预测)

基于 JD 要求 + 项目技术栈，预测面试可能问的技术问题。

### 触发条件
- 用户说"面试会问什么""技术问题""帮我准备面试"
- 也可在 JD 解析结束后主动提示："要不要看看这个岗位可能会问什么技术问题？"

### 输入
- JD 岗位画像（来自 Stage 1 或独立输入的 JD）
- 项目技术栈（来自 Stage 2 扫描结果，或用户手动描述）

### 处理
参考 `interview-prep.md` 中的预测规则:
1. 对每个 must-have 技能生成 2-3 个分层问题（基础/中等/深入）
2. 对项目中使用的每个技术生成项目相关追问
3. 加入通用软技能问题
4. 按优先级排序（JD 高频 + 项目使用 > JD 高频 > 项目使用 > 软技能）

### 向用户展示
> "基于这个岗位的要求和你的项目经历，我预测了以下面试问题。按优先级从高到低排列——标红的题目建议重点准备。"

```

- [ ] **Step 3: Verify**

Run: `grep -c "Interview Prep" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 4: Commit B2**

```bash
git add resume-star/interview-prep.md resume-star/SKILL.md
git commit -m "feat(B2): add interview question prediction — JD + project-based question generation"
```

---

### Task 9: Create interview-sim.md (B1+B3 — P5+P6)

**Files:**
- Create: `resume-star/interview-sim.md`

- [ ] **Step 1: Write interview-sim.md**

Create `resume-star/interview-sim.md` with the following content:

```markdown
# Interview Simulation & Oral Training Reference

## Mock Interview (面试模拟)

### 模拟流程

1. Skill 从已生成的 STAR 展开中选取一个亮点作为模拟话题
2. Skill 扮演面试官，先问一个开放性问题（如"介绍一下你最有成就感的项目"）
3. 用户回答后，Skill 基于回答内容进行追问
4. 每轮追问后给出**回答参考**和**改进建议**
5. 用户可随时输入"退出模拟"结束

### 追问类型

| 类型 | 目的 | 示例 |
|------|------|------|
| 技术深度 | 检验真实理解 | "为什么选 ANTLR4 而不是手写 parser？" |
| 结果量化 | 验证数字来源 | "98% 准确率是怎么算的？对比基线是什么？" |
| 替代方案 | 检验思考深度 | "如果不能用 Redis，你会怎么解决这个缓存问题？" |
| 困难挑战 | 考察问题解决能力 | "这个项目中遇到最大的技术难点是什么？" |
| 团队协作 | 考察软技能 | "你和队友在技术方案上有过分歧吗？怎么解决的？" |

### 回答评价维度

对用户的每轮回答，从以下维度给出反馈:

1. **完整性:** 是否覆盖了 S-T-A-R 四要素
2. **具体性:** 有没有具体技术细节，还是只停留在"我做了 X"
3. **量化性:** 结果有没有数据支撑
4. **流畅性:** 表达是否清晰有条理
5. **匹配性:** 回答是否切中面试官问题的核心

### 反馈格式

```
## 回答反馈

**整体评价:** [好/一般/需要改进]

**做得好的地方:**
- [具体反馈]

**可以改进的地方:**
- [具体反馈 + 改进建议]

**参考回答:**
> [一个高质量的回答示例，用户可以学习表述方式]

**追问:** [下一个问题]
```

---

## Oral Training (口述训练)

### 口述脚本生成

将 Bullet Point 转化为自然口语风格的脚本，提供两个版本:

#### 1 分钟版（项目概述）

适用场景: "介绍一下你最有成就感的项目"

格式要求:
- 开头: 一句话说项目是什么 + 解决什么问题
- 中间: 你负责的部分 + 关键技术决策（只说 1-2 个最重要的）
- 结尾: 一个可量化的成果
- 语气: 自然口语，不念稿，用"我当时负责...""我的做法是..."

#### 3 分钟版（详细展开）

适用场景: 面试官追问细节时

格式要求:
- 完整的 S-T-A-R 结构，但用口语化表达
- 每个要点之间有自然的过渡（"在这个过程中...""当时遇到的一个问题是..."）
- 技术细节可以展开，但要先说"为什么"再说"怎么做"
- 结尾回到成果，最好有一个数字

### 口述技巧提醒

生成口述脚本时附带以下提醒:

1. **停顿标记:** 在关键转折点标注 [停顿]，提醒用户在这里可以观察面试官反应
2. **强调标记:** 在核心成果或关键技术决策处标注 [强调]，提醒用户加重语气
3. **防跑题提醒:** 列出容易跑题的点（如"不要在技术细节上讲太久不回到结果"）
4. **口语化提醒:** 避免"然后...然后..."、"就是...就是说..."、"对对对"等口语赘词

### Output Format

```markdown
## 口述脚本 — [项目名称]

### 1 分钟版（项目概述）

> "我做过一个 [项目简述]。当时 [背景/Situation]。我主要负责 [任务/Task]，用了 [关键技术方案/Action]。最终 [结果/Result，包含量化数据]。"
>
> [停顿] 观察面试官反应，如果他感兴趣会追问细节 → 切换到 3 分钟版

### 3 分钟版（详细展开）

> "这个项目的背景是 [展开 Situation]...
>
> 我当时负责的部分是 [展开 Task]...
>
> [强调] 我的做法是 [展开 Action，包括技术选型理由、实现细节、遇到的问题和解决方案]...
>
> 最终 [展开 Result，包含量化数据和对比]。"

### 口述技巧
- [停顿点]: [在哪里停顿，为什么]
- [强调点]: [在哪里加重语气，为什么]
- 防跑题: [容易跑题的点提醒]
```

## Example: Oral Script

**基于 Example 1（编译器项目）:**

### 1 分钟版

> "我做过一个 Mini-Java 编译器，是编译原理课的课程项目。我负责语法分析和类型检查这两个核心模块。用了 ANTLR4 来生成语法树，然后手写了 Visitor 模式来实现类型推断，支持泛型。最终通过了 200 个测试用例，类型推断准确率 98%。"

### 3 分钟版

> "这个项目是我们编译原理课的大作业，要求实现一个支持类型推断的 Mini-Java 编译器前端。
>
> 我负责的是语法分析和类型检查这两个最核心的模块。语法分析这块，[强调] 我选了 ANTLR4 而不是手写递归下降，因为 Mini-Java 的语法规则比较多，用工具生成更不容易出错。[停顿]
>
> 类型推断是难点，我用了 Visitor 模式遍历语法树来做类型推导。最棘手的是泛型的协变和逆变，[强调] 我查了 Java Language Spec 的相关章节才搞清楚规则。
>
> 最后测试覆盖了 50 多个边界用例，[强调] 全部 200 个测试用例通过，类型推断准确率 98%，拿到了课程最高分。"
```

- [ ] **Step 2: Verify file exists**

Run: `head -3 resume-star/interview-sim.md`
Expected: Shows "# Interview Simulation & Oral Training Reference"

---

### Task 10: Add interview simulation and oral training flow to SKILL.md (B1+B3 — P5+P6)

**Depends on:** Task 9

**Files:**
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add interview sim triggers to "When to Use"**

In SKILL.md, find the `## When to Use` section. Add:

```markdown
- 用户说"模拟面试""练一下项目介绍""帮我练口语"
- 用户想准备面试，需要练习项目经历的口头表达
```

- [ ] **Step 2: Add interview simulation flow section**

In SKILL.md, find the `## Interview Prep` section. Insert the following AFTER it (before Resume Review):

```markdown
## Interview Simulation (面试模拟 + 口述训练)

基于已生成的 STAR 展开部分，进行模拟面试追问和口述训练。

### 触发条件
- 用户说"模拟面试""练一下""帮我练口语"
- STAR 生成结束后主动提示："要不要针对这条练一下面试回答？"

### 两种模式

#### 模式 A: 面试模拟（对话式）

参考 `interview-sim.md` 中的模拟流程:

1. 从 STAR 展开中选取一个亮点作为话题
2. 扮演面试官，先问开放性问题
3. 用户回答后追问（技术深度 / 结果量化 / 替代方案 / 困难挑战）
4. 每轮给出回答反馈 + 参考回答 + 下一个追问
5. 用户输入"退出模拟"结束

#### 模式 B: 口述训练（脚本生成）

参考 `interview-sim.md` 中的口述脚本规则:

1. 将 Bullet Point 转化为 1 分钟版口述脚本（项目概述）
2. 同时提供 3 分钟版口述脚本（详细展开）
3. 附带口述技巧提醒（停顿点、强调点、防跑题提醒）
4. 用户可以要求调整口述风格

### 向用户展示
> "我可以帮你练一下项目介绍。你想先模拟面试（我来追问），还是先生成口述脚本（你自己练）？"

```

- [ ] **Step 3: Verify**

Run: `grep -c "Interview Simulation" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 4: Commit B1+B3**

```bash
git add resume-star/interview-sim.md resume-star/SKILL.md
git commit -m "feat(B1+B3): add mock interview simulation and oral training with scripts"
```

---

### Task 11: Sync to .claude/skills/ and final commit

**Depends on:** All previous tasks

**Files:**
- Sync: `.claude/skills/resume-star/`

- [ ] **Step 1: Sync all skill files to installed location**

```bash
cp resume-star/SKILL.md .claude/skills/resume-star/SKILL.md
cp resume-star/jd-analysis.md .claude/skills/resume-star/jd-analysis.md
cp resume-star/project-scan.md .claude/skills/resume-star/project-scan.md
cp resume-star/star-examples.md .claude/skills/resume-star/star-examples.md
cp resume-star/interview-prep.md .claude/skills/resume-star/interview-prep.md
cp resume-star/interview-sim.md .claude/skills/resume-star/interview-sim.md
```

- [ ] **Step 2: Verify file count**

Run: `ls resume-star/ | wc -l`
Expected: 6

Run: `ls .claude/skills/resume-star/ | wc -l`
Expected: 6

- [ ] **Step 3: Final commit**

```bash
git add resume-star/ .claude/skills/resume-star/
git commit -m "chore: sync all expanded skill files to installed location"
```

---

## Parallelism Map

```
Task 1 (jd-analysis.md English)     ──┐
Task 2 (star-examples.md English)   ──┤  ← parallel
                                       │
                                  Task 3 (SKILL.md language detection — depends on 1,2)
                                       │
                                  Task 4 (SKILL.md resume review — independent)
                                       │
Task 5 (star-examples.md batch)     ──┐
                                       │
                                  Task 6 (SKILL.md batch mode — depends on 5)
                                       │
Task 7 (interview-prep.md)          ──┐
                                       │
                                  Task 8 (SKILL.md interview prep — depends on 7)
                                       │
Task 9 (interview-sim.md)           ──┐
                                       │
                                  Task 10 (SKILL.md interview sim — depends on 9)
                                       │
                                  Task 11 (sync + final commit — depends on all)
```

Parallel opportunities:
- Task 1 + Task 2: fully independent (different files)
- Task 4: independent of Tasks 1-3 (different section of SKILL.md)
- Task 7 + Task 9: fully independent (new files, no overlap)
