# Resume-Star Next Iteration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Deepen the resume-star Skill with 5 expansion points: code evidence chain, git contribution analysis, project highlight classification, bullet point quality scoring, and JD style strategy table.

**Architecture:** All changes are incremental edits to existing Markdown skill files in `resume-star/`. No code, no tests, no build system. Each task modifies specific sections of specific files with concrete content.

**Tech Stack:** Markdown (Claude Code Skill). Validation is manual: trigger the skill in Claude Code with real inputs.

---

## File Structure

```
resume-star/
├── SKILL.md              # [MODIFY] Task 2 (git confirmation), Task 4 (quality output)
├── jd-analysis.md        # [MODIFY] Task 5 (style strategy table)
├── project-scan.md       # [MODIFY] Task 1 (evidence chain), Task 2 (git analysis), Task 3 (classification)
├── star-examples.md      # [MODIFY] Task 3 (dimension mapping), Task 4 (quality scoring)
├── interview-prep.md     # [UNCHANGED]
└── interview-sim.md      # [UNCHANGED]
```

**Decomposition rationale:**
- Tasks 1 and 2 both modify project-scan.md but touch different sections (highlights vs git), so sequential execution is safe
- Task 5 (jd-analysis.md) is fully independent of Tasks 1-4 (different file)
- SKILL.md changes in Task 2 and Task 4 touch different stages (Stage 2 vs Stage 3), no overlap

---

### Task 1: Add code evidence chain to project-scan.md (P0)

**Files:**
- Modify: `resume-star/project-scan.md`

- [ ] **Step 1: Add evidence extraction rules**

In `resume-star/project-scan.md`, find the `## Highlight Extraction Rules` section. After the existing rule 5 ("**量化数据采集:**..."), add rule 6:

```markdown
6. **代码证据定位:** 每个亮点必须关联关键源文件路径
   - 证据来源优先级:
     1. 从 Glob/Grep 结果的文件名直接推断（如 `ExceptionHandler.java` → 异常处理亮点）
     2. 从 README / 配置文件中提取的功能描述对应到源文件
     3. 从目录结构推断的模块职责（如 `src/auth/` → 认证模块）
   - 每个亮点最多列出 3 个关键文件路径
   - 路径使用相对于项目根目录的相对路径
   - 如果扫描阶段无法定位具体文件，该亮点标记为"（基于用户描述）"
```

- [ ] **Step 2: Update output format to include evidence**

In `resume-star/project-scan.md`, find the `## Output Format` section. Replace the "### 发现的亮点" subsection with:

```markdown
### 发现的亮点（含代码证据）
1. **[亮点标题]** — [简述: 做了什么, 用了什么技术]
   - 证据: [相对路径1], [相对路径2]
2. **[亮点标题]** — [简述]
   - 证据: [相对路径1]
3. **[亮点标题]** — [简述]（基于用户描述）
   - 证据: 无本地文件，需要用户确认
```

- [ ] **Step 3: Verify file structure**

Run: `grep -c "代码证据定位" resume-star/project-scan.md`
Expected: 1

- [ ] **Step 4: Commit**

```bash
git add resume-star/project-scan.md
git commit -m "feat(P0): add code evidence chain to project scan highlights"
```

---

### Task 2: Add git contribution analysis to project-scan.md + SKILL.md (P0)

**Depends on:** Task 1 (same file, sequential)

**Files:**
- Modify: `resume-star/project-scan.md`
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Expand git scan step in project-scan.md**

In `resume-star/project-scan.md`, find `### Step 5: Git Log (optional)`. Replace the entire step with:

```markdown
### Step 5: Git Contribution Analysis (optional, 仅 Git 仓库)

如果项目是 Git 仓库，执行以下分析:

```
命令序列:
  1. git -C <project_path> log --oneline -20
     → 最近 20 条提交概览
  2. git -C <project_path> log --stat --oneline -10
     → 带文件变更的提交记录
  3. git -C <project_path> shortlog -sn
     → 按作者统计提交数
  4. git -C <project_path> log --format="%H %ai" --follow -- <高频修改的文件> | head -10
     → 关键文件的修改历史
如果失败（非 Git 仓库）: 跳过，不影响扫描
```

分析目标:
- 开发周期（从最早和最晚提交推断）
- 贡献者数量和各自的提交占比
- 高频修改模块（从 `--stat` 中统计文件路径出现频率）
- 用户的实际贡献范围（从 shortlog 中识别主要作者）

注意:
- 不分析具体代码 diff 内容（节省 token），只看文件路径和提交频率
- 如果只有一个作者，不需要区分贡献
- 统计数据仅作为参考，最终以用户确认为准
```

- [ ] **Step 2: Add git output format to project-scan.md**

In `resume-star/project-scan.md`, find the `## Output Format` section. After the `### 量化数据（从扫描中提取）` subsection, add:

```markdown

### Git 贡献分析（仅 Git 仓库显示）
- 开发周期：[起始日期] - [结束日期]
- 总提交数：[N]（用户占 [M]）
- 贡献者：[名字1]([X]次), [名字2]([Y]次)
- 高频修改模块：[模块1], [模块2], [模块3]
- 用户主要贡献：[基于高频修改文件推断的职责描述]
```

- [ ] **Step 3: Add git confirmation step to SKILL.md Stage 2**

In `resume-star/SKILL.md`, find the `## Stage 2: 项目扫描` section. Find the line:

```
> "我从你的项目中发现这些亮点：A、B、C。你觉得哪个最值得展开？有没有我遗漏的？"
```

Replace it with:

```
> "我从你的项目中发现这些亮点：A、B、C。你觉得哪个最值得展开？有没有我遗漏的？"
>
> 如果 Git 分析显示多人贡献:
> "我分析了项目的 Git 记录。看起来你主要贡献了 [模块列表]，占总提交的 [X]%。这样理解对吗？如果项目不是你一个人的，告诉我你负责的部分。"
```

- [ ] **Step 4: Verify both files**

Run: `grep -c "Git Contribution Analysis" resume-star/project-scan.md`
Expected: 1

Run: `grep -c "Git 分析" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 5: Commit**

```bash
git add resume-star/project-scan.md resume-star/SKILL.md
git commit -m "feat(P0): add git contribution analysis with multi-author detection"
```

---

### Task 3: Add project highlight classification to project-scan.md + star-examples.md (P1)

**Depends on:** Task 2 (same file, sequential)

**Files:**
- Modify: `resume-star/project-scan.md`
- Modify: `resume-star/star-examples.md`

- [ ] **Step 1: Add classification rules to project-scan.md**

In `resume-star/project-scan.md`, find the `## Highlight Extraction Rules` section. After the `6. **代码证据定位:**` rule added in Task 1, add:

```markdown

## Highlight Classification Rules

每个提取的亮点必须标注一个主要分类维度:

| 维度 | 识别信号 | 典型关键词/文件模式 |
|------|---------|-------------------|
| 技术亮点 | 技术选型决策、非平凡实现 | 新框架引入、自定义算法、中间件集成 |
| 性能亮点 | 明确的性能改进、资源优化 | 缓存、索引、异步、批处理、压缩、连接池 |
| 工程化亮点 | 代码规范、自动化、可维护性 | CI/CD、统一异常处理、代码分层、测试覆盖 |
| 业务亮点 | 功能完整度、用户流程闭环 | 完整的 CRUD、支付流程、用户注册到使用闭环 |
| 安全亮点 | 认证鉴权、数据保护 | JWT、OAuth、加密、输入校验、权限控制 |
| 数据亮点 | 数据处理规模、存储优化 | ETL、数据清洗、批量导入、分表分库 |

分类规则:
- 一个亮点可以有 1 个主分类 + 1 个副分类
- 如果无法判断，默认归为"技术亮点"
- 分类结果用于后续 STAR 生成时的维度匹配
```

- [ ] **Step 2: Update highlight output format with classification**

In `resume-star/project-scan.md`, find the `### 发现的亮点（含代码证据）` subsection (added in Task 1). Replace it with:

```markdown
### 发现的亮点（含分类和代码证据）
1. **[亮点标题]** `[主分类/副分类]` — [简述: 做了什么, 用了什么技术]
   - 证据: [相对路径1], [相对路径2]
2. **[亮点标题]** `[主分类]` — [简述]
   - 证据: [相对路径1]
3. **[亮点标题]** `[主分类]` — [简述]（基于用户描述）
```

- [ ] **Step 3: Add dimension-to-JD mapping to star-examples.md**

In `resume-star/star-examples.md`, find the `## Batch Output Format` section. Before it, add:

```markdown

## Highlight Dimension Matching

当已知岗位类型时，按以下优先级推荐突出维度:

| 岗位类型 | 优先突出的亮点维度 | 次优维度 |
|----------|-------------------|---------|
| 后端开发 | 技术亮点 > 性能亮点 > 工程化亮点 | 数据亮点 |
| 前端开发 | 业务亮点 > 技术亮点 > 工程化亮点 | 性能亮点 |
| 算法/数据 | 数据亮点 > 技术亮点 > 性能亮点 | 工程化亮点 |
| 产品经理 | 业务亮点 > 数据亮点 | 技术亮点 |
| 测试开发 | 工程化亮点 > 技术亮点 | 安全亮点 |
| 运维/DevOps | 工程化亮点 > 性能亮点 > 安全亮点 | 技术亮点 |
| AI/大模型应用 | 技术亮点 > 数据亮点 > 性能亮点 | 工程化亮点 |

使用规则:
- 从项目亮点中筛选匹配 JD 岗位类型的维度，优先展示
- 用户也可手动指定: "重点突出工程化方面的亮点"
- 如果某个维度无亮点，跳过该维度，不强行编造
```

- [ ] **Step 4: Verify both files**

Run: `grep -c "Highlight Classification Rules" resume-star/project-scan.md`
Expected: 1

Run: `grep -c "Highlight Dimension Matching" resume-star/star-examples.md`
Expected: 1

- [ ] **Step 5: Commit**

```bash
git add resume-star/project-scan.md resume-star/star-examples.md
git commit -m "feat(P1): add highlight classification with dimension-to-JD mapping"
```

---

### Task 4: Add bullet point quality scoring to star-examples.md + SKILL.md (P2)

**Depends on:** Task 3 (star-examples.md sequential)

**Files:**
- Modify: `resume-star/star-examples.md`
- Modify: `resume-star/SKILL.md`

- [ ] **Step 1: Add quality scoring rules to star-examples.md**

In `resume-star/star-examples.md`, find the `## Highlight Dimension Matching` section (added in Task 3). Before it, add:

```markdown

## Bullet Point Quality Scoring

对生成的每条 Bullet Point 进行自评，在输出末尾附带质量评估。

### 评分维度

| 维度 | 满分 | 评判标准 |
|------|------|---------|
| 完整性 | 10 | 是否包含: 动词 + 做了什么 + 怎么做 + 结果 |
| 岗位匹配度 | 10 | 是否命中 JD must-have 技能 |
| 技术含量 | 10 | 是否有具体技术细节（方案、工具、原理），而非空泛描述 |
| 量化程度 | 10 | 结果是否有数据支撑。无数据不扣分，编造数据直接标红警告 |
| 面试可解释性 | 10 | 用户能否在面试中用 STAR 复述并解释每个技术点 |

### 评分规则

- 每个维度独立评分，不打总分（避免总分掩盖单项短板）
- **量化程度特殊规则:**
  - 有真实量化数据 → 8-10 分
  - 无数据但有定性成果 → 5-7 分
  - 无法从项目扫描结果中找到数据来源的量化数字 → 标记 "⚠️ 数据来源不明，建议确认"
  - 编造嫌疑的数字（如"提升 200%"且无依据）→ 标记 "🚫 疑似编造，必须删除或替换"
- **面试可解释性评判:** 用户是否能回答"为什么选这个方案""遇到了什么困难""效果怎么衡量的"

### 输出格式

在 STAR 生成的所有 Bullet Point 和 STAR 展开之后，附上:

```markdown
---

## 质量评估

| # | 完整性 | 匹配度 | 技术含量 | 量化 | 可解释性 | 建议 |
|---|--------|--------|----------|------|----------|------|
| 1 | 8/10   | 9/10   | 7/10     | 5/10 | 8/10     | 补充接口响应速度或代码复用率 |
| 2 | 9/10   | 8/10   | 8/10     | 7/10 | 9/10     | 良好 |
| 3 | 7/10   | 6/10   | 6/10     | 3/10 | 7/10     | 结果偏空泛，建议补充功能覆盖范围 |

**整体建议:** 第 3 条描述的量化程度最低，可补充"覆盖 X 个接口"或"支持 Y 种导出格式"。
```

### 自评触发规则

- 自评在 STAR 生成后自动附带，不需要用户额外触发
- 用户可以要求"重新生成得分最低的那条"
- 自评基于内容本身质量，不受项目大小影响（小项目也可以高分）
```

- [ ] **Step 2: Add quality scoring output to SKILL.md Stage 3**

In `resume-star/SKILL.md`, find the `## Stage 3: STAR 生成` section. Find the `## Output Format` section. Insert a new section BEFORE `## Output Format`:

```markdown

## Quality Scoring (子弹点质量自评)

STAR 生成后自动附带质量评估，不需要用户触发。

### 流程
1. 对每条生成的 Bullet Point 按五维度评分（完整性、匹配度、技术含量、量化、可解释性）
2. 评分规则参考 `star-examples.md` 的 Bullet Point Quality Scoring 部分
3. 对得分最低的 1-2 条给出具体改进建议
4. 如果检测到量化数据无法溯源，标记警告

### 向用户展示
> "这是你的简历素材和自评结果。第 [N] 条建议补充量化数据，你可以告诉我实际的数据，或者我帮你调整表述。"
```

- [ ] **Step 3: Verify both files**

Run: `grep -c "Bullet Point Quality Scoring" resume-star/star-examples.md`
Expected: 1

Run: `grep -c "Quality Scoring" resume-star/SKILL.md`
Expected: 1

- [ ] **Step 4: Commit**

```bash
git add resume-star/star-examples.md resume-star/SKILL.md
git commit -m "feat(P2): add bullet point quality scoring with five-dimension evaluation"
```

---

### Task 5: Add JD style strategy table to jd-analysis.md (P3)

**Files:**
- Modify: `resume-star/jd-analysis.md`

This task is fully independent of Tasks 1-4 (different file). Can run in parallel.

- [ ] **Step 1: Add style classification and strategy table**

In `resume-star/jd-analysis.md`, find the `## Output Format` section. Before it, add:

```markdown

## JD Style Classification

### 风格类型与识别信号

| JD 风格 | 识别信号词 | 典型来源 |
|---------|-----------|---------|
| 大厂校招型 | "校招"、"应届"、"202X届"、"培养体系"、"成长"、"导师" | 大厂校园招聘页面 |
| 创业公司实战型 | "0到1"、"快速迭代"、"多面手"、"全栈"、"拥抱变化"、"小团队" | 早期创业公司 JD |
| 技术深度型 | "原理"、"源码"、"优化"、"架构设计"、"底层"、"深入理解" | 技术驱动型团队 |
| 业务导向型 | "用户体验"、"业务价值"、"数据驱动"、"增长"、"ROI"、"指标" | 业务导向型团队 |
| 外企英文型 | JD 全英文、"global"、"communication"、"English" | 外企或出海公司 |
| 工程规范型 | "CI/CD"、"代码审查"、"测试覆盖"、"SOP"、"规范"、"流程" | 成熟工程团队 |

### 风格对应的表达策略

| JD 风格 | 简历表达重点 | Bullet Point 侧重点 | STAR 展开重点 |
|---------|------------|-------------------|-------------|
| 大厂校招型 | 基础扎实、学习能力、项目完整度、工程规范 | 强调"学"+"做"的完整过程 | 重点展开学习路径和技术理解过程 |
| 创业公司实战型 | 独立负责、快速交付、业务结果、跨职能 | 强调"独立完成"+"业务效果" | 重点展开独立决策和快速落地的过程 |
| 技术深度型 | 技术难点、方案对比、性能数据、架构决策 | 强调"为什么选这个方案"+"量化效果" | 重点展开技术选型理由和优化细节 |
| 业务导向型 | 业务闭环、用户影响、数据指标、产品思维 | 强调"业务价值"+"用户影响" | 重点展开业务场景和效果指标 |
| 外企英文型 | 职责边界清晰、结果导向、避免堆砌技术词 | 英文输出，contribution > technology | 用英文展开，强调 ownership 和 impact |
| 工程规范型 | 工程化实践、代码质量、协作流程、文档习惯 | 强调"流程"+"规范"+"自动化" | 重点展开工程实践和团队协作方式 |

### 同一亮点的风格化改写示例

以 Redis 缓存优化为例:

| JD 风格 | 改写版本 |
|---------|---------|
| 大厂校招型 | 学习并应用 Redis 缓存机制，降低数据库查询频率，提升系统响应速度 |
| 技术深度型 | 基于 Redis 设计多级缓存策略，通过缓存预热和懒加载机制降低数据库查询压力约 60% |
| 创业实战型 | 独立完成 Redis 缓存模块设计和上线，首页加载速度显著提升，支撑产品快速迭代 |
| 业务导向型 | 引入 Redis 缓存优化核心业务查询链路，用户页面加载等待时间明显缩短，提升用户留存 |

### 输出集成

在岗位画像末尾附加风格判断:

```
### JD 风格判断
- 风格：[风格类型]
- 信号词：[匹配到的信号词列表]
- 建议表达重点：[对应的表达策略摘要]
```

```

- [ ] **Step 2: Verify file**

Run: `grep -c "JD Style Classification" resume-star/jd-analysis.md`
Expected: 1

- [ ] **Step 3: Commit**

```bash
git add resume-star/jd-analysis.md
git commit -m "feat(P3): add JD style classification with expression strategy table"
```

---

### Task 6: Sync to .claude/skills/ and final commit

**Depends on:** All previous tasks

**Files:**
- Sync: `.claude/skills/resume-star/`

- [ ] **Step 1: Sync all modified skill files**

```bash
cp resume-star/SKILL.md .claude/skills/resume-star/SKILL.md
cp resume-star/jd-analysis.md .claude/skills/resume-star/jd-analysis.md
cp resume-star/project-scan.md .claude/skills/resume-star/project-scan.md
cp resume-star/star-examples.md .claude/skills/resume-star/star-examples.md
```

- [ ] **Step 2: Verify file count and sync**

Run: `ls resume-star/ | wc -l`
Expected: 6

Run: `diff resume-star/SKILL.md .claude/skills/resume-star/SKILL.md`
Expected: no output (identical)

Run: `diff resume-star/project-scan.md .claude/skills/resume-star/project-scan.md`
Expected: no output (identical)

Run: `diff resume-star/star-examples.md .claude/skills/resume-star/star-examples.md`
Expected: no output (identical)

Run: `diff resume-star/jd-analysis.md .claude/skills/resume-star/jd-analysis.md`
Expected: no output (identical)

- [ ] **Step 3: Final commit**

```bash
git add resume-star/ .claude/skills/resume-star/
git commit -m "chore: sync all updated skill files to installed location"
```

---

## Parallelism Map

```
Task 1 (project-scan.md evidence)  ──┐
                                      ├── Task 2 (project-scan.md git + SKILL.md Stage 2)
                                      │
                                 Task 3 (project-scan.md classification + star-examples.md) ──┐
                                                                                               │
                                                                                          Task 4 (star-examples.md scoring + SKILL.md Stage 3)

Task 5 (jd-analysis.md style)       ── fully independent, can run in parallel with all above

                                 Task 6 (sync + final commit — depends on all)
```

Parallel opportunities:
- Task 5 is fully independent (different file), can run alongside Tasks 1-4
- Tasks 1-4 are sequential due to file dependencies (same files modified in order)
