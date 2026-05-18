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

### Step 5: Git Log (optional)
```
命令: bash: git -C <project_path> log --oneline -20
目标: 了解开发活跃度和贡献范围
关注: commit 频率、涉及的功能模块
如果失败（非 Git 仓库）: 跳过，不影响扫描
```

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

## Output Format

向用户展示的项目亮点列表格式:

```
## 项目扫描: [项目名称]

### 基本信息
- 类型: [前端/后端/全栈/...]
- 技术栈: [语言] + [框架] + [关键依赖]
- 项目结构: [简要描述目录组织]

### 发现的亮点（含代码证据）
1. **[亮点标题]** — [简述: 做了什么, 用了什么技术]
   - 证据: [相对路径1], [相对路径2]
2. **[亮点标题]** — [简述]
   - 证据: [相对路径1]
3. **[亮点标题]** — [简述]（基于用户描述）
   - 证据: 无本地文件，需要用户确认

### 可能遗漏
- [提示用户补充可能没被扫描到的信息]

### 量化数据（从扫描中提取）
- 源码文件数: [N]
- 代码行数: [约 N 行]
- 核心模块数: [N]
- API 接口数: [N]（如有路由文件可统计）
- 测试文件数: [N]
```

## Fallback: 无本地项目

如果用户没有本地项目或项目过于简单:

1. 直接询问用户: "请描述一下你参与的项目——做了什么功能、用了什么技术、解决了什么问题？"
2. 基于用户描述提取亮点，跳过文件扫描
3. 继续进入 STAR 生成阶段
