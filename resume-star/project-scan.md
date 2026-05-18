# Project Scan Reference

## Project Type Identification

检查项目根目录的特征文件来判断项目类型:

| 特征文件 | 项目类型 | 关键扫描目标 |
|----------|---------|------------|
| package.json | 前端 / Node.js 后端 / 全栈 | dependencies, scripts, README |
| requirements.txt / setup.py / pyproject.toml | Python 项目 | 依赖列表, README |
| pom.xml / build.gradle | Java 项目 | dependencies, README |
| go.mod | Go 项目 | dependencies, README |
| Cargo.toml | Rust 项目 | dependencies, README |
| pubspec.yaml | Flutter / Dart | dependencies, README |
| *.xcodeproj / *.xcworkspace | iOS 项目 | README |
| docker-compose.yml | 有容器化部署 | 额外加 1 分（可写进简历） |

## Scan Sequence

按以下顺序扫描，每步收集信息后判断是否需要继续:

### Step 1: Directory Structure
```
命令: ls -la <project_path>
目标: 了解顶层目录布局
关注: src/, lib/, app/, api/, config/, test/ 等常见目录
```

### Step 2: Config Files (技术栈)
```
命令: glob <project_path>/{package.json,requirements.txt,pyproject.toml,pom.xml,build.gradle,go.mod,Cargo.toml,pubspec.yaml,Gemfile,*.csproj}
目标: 确定语言、框架、主要依赖
关注: dependencies/devDependencies 中的框架和库
```

### Step 3: README
```
命令: read <project_path>/README.md
目标: 了解项目目的、功能描述、架构说明
关注: 项目简介、功能列表、技术架构描述
```

### Step 4: Key Source Files
```
命令: glob <project_path>/src/**/*.{java,py,js,ts,go,rs} 或对应语言扩展名
目标: 识别核心功能模块
关注: 文件/目录命名反映的功能（如 auth/, payment/, search/）
      路由文件（router, urls, routes）反映的功能范围
```

### Step 5: Git Contribution Analysis (optional, 仅 Git 仓库)

如果项目是 Git 仓库，执行以下分析:

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

分析目标:
- 开发周期（从最早和最晚提交推断）
- 贡献者数量和各自的提交占比
- 高频修改模块（从 `--stat` 中统计文件路径出现频率）
- 用户的实际贡献范围（从 shortlog 中识别主要作者）

注意:
- 不分析具体代码 diff 内容（节省 token），只看文件路径和提交频率
- 如果只有一个作者，不需要区分贡献
- 统计数据仅作为参考，最终以用户确认为准

### Step 6: Quantification Scan (required)
```
目标: 收集可写入简历的量化数据
命令序列:
  1. bash: find <project_path> -name "*.py" -o -name "*.java" -o -name "*.js" -o -name "*.ts" -o -name "*.go" -o -name "*.rs" | wc -l
     → 源码文件数
  2. bash: find <project_path> -name "test_*" -o -name "*_test.*" -o -name "*Test.*" -o -name "test" -type d | head -20
     → 测试文件/目录，可推断测试覆盖情况
  3. bash: find <project_path> -name "*.py" -o -name "*.java" -o -name "*.js" -o -name "*.ts" | xargs wc -l 2>/dev/null | tail -1
     → 总代码行数（大致）
  4. glob <project_path>/**/CLAUDE.md
     → 项目文档中的规模描述
关注: 任何可以量化的数字——文件数、模块数、API 接口数、测试用例数、代码行数
```

## Highlight Extraction Rules

从扫描结果中提取亮点，按以下优先级:

1. **解决了什么问题:** README 或 commit message 中描述的业务问题
2. **用了什么技术:** 从 config 文件中提取的技术栈，特别是有亮点的技术（如用了 Redis 做缓存、用了消息队列）
3. **做了什么功能:** 从目录结构和路由文件中推断的功能模块
4. **有什么规模:** 数据量、并发量、用户量等可量化的指标（如果有）
5. **量化数据采集:** 从 Step 6 中收集到的数字（文件数、代码行数、模块数、API 数、测试数）必须记录在亮点中
6. **代码证据定位:** 每个亮点必须关联关键源文件路径
   - 证据来源优先级:
     1. 从 Glob/Grep 结果的文件名直接推断（如 `ExceptionHandler.java` → 异常处理亮点）
     2. 从 README / 配置文件中提取的功能描述对应到源文件
     3. 从目录结构推断的模块职责（如 `src/auth/` → 认证模块）
   - 每个亮点最多列出 3 个关键文件路径
   - 路径使用相对于项目根目录的相对路径
   - 如果扫描阶段无法定位具体文件，该亮点标记为"（基于用户描述）"

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

## Output Format

向用户展示的项目亮点列表格式:

```
## 项目扫描: [项目名称]

### 基本信息
- 类型: [前端/后端/全栈/...]
- 技术栈: [语言] + [框架] + [关键依赖]
- 项目结构: [简要描述目录组织]

### 发现的亮点（含分类和代码证据）
1. **[亮点标题]** `[主分类/副分类]` — [简述: 做了什么, 用了什么技术]
   - 证据: [相对路径1], [相对路径2]
2. **[亮点标题]** `[主分类]` — [简述]
   - 证据: [相对路径1]
3. **[亮点标题]** `[主分类]` — [简述]（基于用户描述）

### 可能遗漏
- [提示用户补充可能没被扫描到的信息]

### 量化数据（从扫描中提取）
- 源码文件数: [N]
- 代码行数: [约 N 行]
- 核心模块数: [N]
- API 接口数: [N]（如有路由文件可统计）
- 测试文件数: [N]

### Git 贡献分析（仅 Git 仓库显示）
- 开发周期：[起始日期] - [结束日期]
- 总提交数：[N]（用户占 [M]）
- 贡献者：[名字1]([X]次), [名字2]([Y]次)
- 高频修改模块：[模块1], [模块2], [模块3]
- 用户主要贡献：[基于高频修改文件推断的职责描述]
```

## Fallback: 无本地项目

如果用户没有本地项目或项目过于简单:

1. 直接询问用户: "请描述一下你参与的项目——做了什么功能、用了什么技术、解决了什么问题？"
2. 基于用户描述提取亮点，跳过文件扫描
3. 继续进入 STAR 生成阶段
