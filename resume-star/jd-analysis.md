# JD Analysis Reference

## Skill Categories

### Hard Skills (直接提取)
- **编程语言:** Java, Python, Go, C++, JavaScript, TypeScript, Rust 等
- **框架/库:** Spring Boot, React, Vue, Django, Express, Flutter 等
- **工具/平台:** Docker, Kubernetes, AWS, MySQL, Redis, Git, CI/CD 等
- **领域知识:** 机器学习、分布式系统、微服务、数据管道 等

### Soft Skills (从描述推断)
- 团队协作: "与跨部门团队合作"、"推动项目落地"
- 问题解决: "排查线上问题"、"优化性能瓶颈"
- 学习能力: "快速上手"、"跟进新技术"
- 沟通表达: "向非技术团队汇报"、"编写技术文档"

### Implicit Requirements (隐性要求)
- 加班/高压: "拥抱变化"、"快速迭代"、"创业氛围"
- 独立性: "独立负责"、"从 0 到 1"
- 全栈能力: 前后端都提到、提到 DevOps

## Weight Assessment Rules

1. **Must-have (必须):** 反复出现的技能、写在"任职要求"第一条的、与岗位核心职责直接相关的
2. **Nice-to-have (加分):** 写在"优先"、"了解"、"熟悉即可"后面的、只出现一次的
3. **Cultural (隐性):** 从公司规模、行业阶段推断的文化偏好

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

## Output Format

向用户展示的岗位画像摘要格式:

```
## 岗位画像: [职位名称] @ [公司名]

### 核心要求 (Must-have)
- [技能1] — [为什么重要]
- [技能2] — [为什么重要]

### 加分项 (Nice-to-have)
- [技能3], [技能4]

### 隐性信号
- [信号1: 推断依据]
- [信号2: 推断依据]

### 匹配建议
这个岗位最看重 [X]，你的项目如果能体现 [Y] 会很有竞争力。
```

## Example: Parsed JD

**输入 (JD 原文片段):**
> 岗位要求: 1. 熟悉 Java 语言，了解 Spring Boot 框架 2. 熟悉 MySQL，有 SQL 调优经验优先 3. 了解 Redis、MQ 等中间件 4. 良好的团队协作能力，能独立完成模块开发 5. 有微服务经验者优先

**输出:**
- Must-have: Java, Spring Boot, MySQL
- Nice-to-have: SQL 调优, Redis, MQ, 微服务
- 隐性信号: "独立完成模块开发" → 需要展示独立负责能力；"微服务优先" → 公司在做服务化改造

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
