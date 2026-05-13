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
