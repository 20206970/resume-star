# Resume-Star-Skill

AI 驱动的简历素材增强工具，基于 [Claude Code Skill](https://docs.anthropic.com/en/docs/claude-code) 实现。

粘贴 JD + 指定本地项目路径 → 对话式生成 STAR 格式简历素材。

## 核心功能

- **JD 解析** — 提取硬/软技能关键词，评估能力权重，识别岗位风格
- **项目扫描** — 分析目录结构、技术栈、核心模块，提取项目亮点
- **STAR 生成** — 基于 JD 要求与项目亮点的匹配，生成 2-3 条 STAR 格式简历描述
- **对话微调** — 每阶段输出均可通过对话确认、修改、回退

## 产品形态

一组 Claude Code Skill 模块（`resume-star/`），直接运行在 Claude Code 环境中，无需额外部署。

利用 Claude Code 内置能力：
- 文件读取（Read、Glob、Grep）扫描项目
- Shell 命令（Bash）执行 `git log` 等
- 网页抓取（WebFetch）获取 JD 链接内容
- 对话交互与用户确认和微调

## 三阶段流程

```
用户输入 JD 文本 + 本地项目路径
        │
        ▼
  阶段 1: JD 解析 → 结构化岗位画像
        │
        ▼
  阶段 2: 项目扫描 → 亮点列表
        │
        ▼
  阶段 3: STAR 生成 → 简历描述块（Markdown）
        │
        ▼
  用户对话微调 → 最终版本
```

## 目标用户

在校生（本科/研究生），有课程项目或实习经历，但不确定如何提炼简历亮点。

## 项目结构

```
resume-star/
  SKILL.md            # 主入口与流程编排
  jd-analysis.md      # JD 解析模块
  project-scan.md     # 项目扫描模块
  star-examples.md    # STAR 示例库
  interview-prep.md   # 面试准备题预测
  interview-sim.md    # 模拟面试
doc/
  产品需求规格说明书.md  # PRD
docs/
  product-design.md    # 产品设计文档
```

## License

MIT
