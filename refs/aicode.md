# AI 编程

## Qwen Code Cli

Qwen Code CLI是一款由阿里巴巴开发的命令行AI编程工具，基于Gemini CLI改造，专为Qwen3-Coder模型优化。它为开发者提供了一个高效、智能的编码辅助环境，支持通过自然语言驱动代码生成与项目管理。

### 为什么选择 Qwen Code

> https://qwenlm.github.io/qwen-code-docs/zh/

- 免费额度： 使用你的 QwenChat  账户，可享受每分钟最多 60 次请求、每天最多 2000 次请求的免费额度。
- 先进模型： 专为 Qwen3-Coder  优化，提供卓越的代码理解和辅助能力。
- 全面功能： 包含 subagents、Plan Mode、TodoWrite、视觉模型支持，以及完整的 OpenAI API 兼容性——所有功能无缝集成。
- 内置 & 可扩展工具： 支持文件系统操作、shell 命令执行、网络抓取/搜索等功能，并可通过 Model Context Protocol (MCP) 轻松扩展，实现自定义集成。
- 面向开发者： 为终端优先的工作流而生——非常适合命令行爱好者。
- 开源： 采用 Apache 2.0 许可证，确保最大程度的自由与透明。

### 安装

#### 系统要求

确保你已安装 Node.js 20  或更高版本。

```sh
node -v
npm -v

# 通过 npm 安装
npm install -g @qwen-code/qwen-code
qwen --version

# 从源码安装
git clone https://github.com/QwenLM/qwen-code.git
cd qwen-code
npm install
npm install -g .

# 使用 Homebrew 全局安装（macOS/Linux）
brew install qwen-code
```

#### 快速开始

```markdown
# 启动 Qwen Code
qwen
 
# 示例命令
> Explain this codebase structure
> Help me refactor this function
> Generate unit tests for this module
```

#### 授权

- Qwen OAuth
首次默认

切换认证 /auth

- OpenAI 兼容 API：
使用 OpenAI 或其他兼容提供商的 API key。
此方法允许你通过 API key 使用多种 AI 模型。

配置方式： 环境变量 或 项目 `.qwen/.env` 文件

项目特定配置

```sh
mkdir -p .qwen
cat >> .qwen/.env <<'EOF'
OPENAI_API_KEY="your-api-key"
OPENAI_BASE_URL="https://api-inference.modelscope.cn/v1"
OPENAI_MODEL="Qwen/Qwen3-Coder-480B-A35B-Instruct"
EOF
```

用户全局配置：

```sh
mkdir -p ~/.qwen
cat >> ~/.qwen/.env <<'EOF'
OPENAI_API_KEY="your-api-key"
OPENAI_BASE_URL="https://dashscope.aliyuncs.com/compatible-mode/v1"
OPENAI_MODEL="qwen3-coder-plus"
EOF
```

非交互模式 / 无头环境


API 提供商选项

> ⚠️地区提示：
>
> - 中国大陆用户：推荐使用阿里云百炼或 ModelScope
> - 国际用户：可使用阿里云 ModelStudio 或 OpenRouter

中国大陆用户
选项 1：**阿里云百炼（申请 API Key ）**

```sh
export OPENAI_API_KEY="your_api_key_here"
export OPENAI_BASE_URL="https://dashscope.aliyuncs.com/compatible-mode/v1"
export OPENAI_MODEL="qwen3-coder-plus"
```

选项 2：**ModelScope（免费额度）（申请 API Key ）**

✅ 每日 2000 次免费调用
⚠️ 需绑定阿里云账号，避免认证错误

```sh
export OPENAI_API_KEY="your_api_key_here"
export OPENAI_BASE_URL="https://api-inference.modelscope.cn/v1"
export OPENAI_MODEL="Qwen/Qwen3-Coder-480B-A35B-Instruct"
```

国际用户
选项 1：**阿里云 ModelStudio（申请 API Key ）**

```sh
export OPENAI_API_KEY="your_api_key_here"
export OPENAI_BASE_URL="https://dashscope-intl.aliyuncs.com/compatible-mode/v1"
export OPENAI_MODEL="qwen3-coder-plus"
```

选项 2：**OpenRouter（提供免费额度）（申请 API Key ）**

```sh
export OPENAI_API_KEY="your_api_key_here"
export OPENAI_BASE_URL="https://openrouter.ai/api/v1"
export OPENAI_MODEL="qwen/qwen3-coder:free"
```

### MCP

github token

### 使用示例

```markdown
cd your-project/
qwen

# 探索代码库

# 架构分析
> Describe the main pieces of this system's architecture
> What are the key dependencies and how do they interact?
> Find all API endpoints and their authentication methods

# 代码开发

# 重构
> Refactor this function to improve readability and performance
> Convert this class to use dependency injection
> Split this large module into smaller, focused components
 
# 代码生成
> Create a REST API endpoint for user management
> Generate unit tests for the authentication module
> Add error handling to all database operations

# 自动化工作流
# Git 自动化
> Analyze git commits from the last 7 days, grouped by feature
> Create a changelog from recent commits
> Find all TODO comments and create GitHub issues

# 文件操作
> 将此目录中的所有图片转换为 PNG 格式 重命名所有测试文件
> 使其符合 *.test.ts 模式 查找并删除所有 console.log 语句

# 调试与分析

# 性能分析
> 识别此 React 组件中的性能瓶颈
> 在代码库中查找所有 N+1 查询问题
 
# 安全审计
> 检查潜在的 SQL 注入漏洞
> 查找所有硬编码的凭证或 API keys

调试与分析

# 性能分析
> 识别此 React 组件中的性能瓶颈
> 在代码库中查找所有 N+1 查询问题
 
# 安全审计
> 检查潜在的 SQL 注入漏洞
> 查找所有硬编码的凭证或 API keys

# 常见任务
# 📚 理解新代码库

> 核心业务逻辑组件有哪些？
> 实现了哪些安全机制？
> 数据在系统中是如何流转的？
> 使用了哪些主要的设计模式？
> 为此模块生成依赖关系图
# 🔨 代码重构与优化

> 这个模块的哪些部分可以优化？
> 帮我重构这个类以遵循 SOLID 原则
> 添加适当的错误处理和日志记录
> 将回调函数转换为 async/await 模式
> 为耗时操作实现缓存机制
# 📝 文档与测试

> 为所有公共 API 生成完整的 JSDoc 注释
> 为此组件编写包含边界情况的单元测试
> 创建 OpenAPI 格式的 API 文档
> 添加内联注释解释复杂算法
> 为此模块生成 README 文件
# 🚀 开发加速

> 设置一个带身份验证的新 Express 服务器
> 创建一个包含 TypeScript 和测试的 React 组件
> 实现限流中间件
> 为新 schema 添加数据库迁移
> 为此项目配置 CI/CD 流水线

```

### 命令与快捷键

Session Commands

- /help - 显示可用命令
- /clear - 清除对话历史
- /compress - 压缩历史记录以节省 token
- /stats - 显示当前会话信息
- /exit 或 /quit - 退出 Qwen Code

Keyboard Shortcuts

- Ctrl+C - 取消当前操作
- Ctrl+D - 退出（在空行时）
- Up/Down - 导航命令历史

## gemini CLI

## Claude Code

AI 编程工具

### 环境准备

Node.js 是运行 Claude Code 的基础环境。

```sh
npm install -g @anthropic-ai/claude-code

claude --version
```

### 接入 DeepSeek

#### 获得账号

访问：https://platform.deepseek.com/

- 18900923186
- 257602@qq.com
- api key: sk-9ad7c0a73c0641f3b607f51b8c9bb92b

#### 配置 claude 环境变量

- windows

打开 PowerShell（需要管理员权限）

```sh
# 注意：setx设置后需重启PowerShell才能生效
setx ANTHROPIC_BASE_URL "https://api.deepseek.com/anthropic"
setx ANTHROPIC_AUTH_TOKEN "sk-9ad7c0a73c0641f3b607f51b8c9bb92b"
setx ANTHROPIC_MODEL "deepseek-chat"
setx ANTHROPIC_SMALL_FAST_MODEL "deepseek-chat"
```

- linux

```sh
export ANTHROPIC_BASE_URL="https://api.deepseek.com/anthropic"
export ANTHROPIC_AUTH_TOKEN="你的DeepSeek API Key"  # 替换成你的真实Key
export ANTHROPIC_MODEL="deepseek-chat"
export ANTHROPIC_SMALL_FAST_MODEL="deepseek-chat"
```

### 接入阿里云百炼的通义千问系列

```sh
setx ANTHROPIC_API_KEY "YOUR_DASHSCOPE_API_KEY"
setx ANTHROPIC_BASE_URL "https://dashscope.aliyuncs.com/apps/anthropic"
setx ANTHROPIC_MODEL "deepseek-chat"
setx ANTHROPIC_SMALL_FAST_MODEL "deepseek-chat"
```

- https://bailian.console.aliyun.com/
- lixiwang@126.com
- sk-82cfc52b33614f1793e5654dfde09f46

https://dashscope.aliyuncs.com/compatible-mode/v1

### 接入胜算云

```sh
setx ANTHROPIC_AUTH_TOKEN "3P-7K3xhJORLF-DhZbTt4nRZsC60Ui60_23IQSoimDCd9yrRJKSvcYHoR7fj4DbChHGzVAZmA-2T_Q"
setx ANTHROPIC_BASE_URL "https://router.shengsuanyun.com/api"
setx ANTHROPIC_MODEL "anthropic/claude-sonnet-4"
setx ANTHROPIC_DEFAULT_HAIKU_MODEL "deepseek/deepseek-v3"
```

### Claude Code Router

安装ccr

```sh
npm install -g @musistudio/claude-code-router
```

### 模搭

### 最佳实践

#### CLAUDE.md

CLAUDE.md 文件是项目级的配置文件，用于为 Claude Code 提供上下文和指导原则。这是确保 AI 理解您的项目结构和编码规范的关键。

> https://aideepcode.cn/best-practices

````markdown
# 项目概述
这是一个 React + TypeScript 的电商平台前端项目

## 技术栈
- React 18 + TypeScript
- Redux Toolkit 状态管理
- Tailwind CSS 样式框架
- Vite 构建工具

## 项目结构
```
src/
├── components/     # 通用组件
├── features/       # 功能模块
├── hooks/         # 自定义 hooks
├── services/      # API 服务
└── utils/         # 工具函数
```

## 编码规范
- 使用函数式组件和 Hooks
- 组件命名使用 PascalCase
- 文件命名使用 kebab-case
- 始终使用 TypeScript 严格类型检查

## 常用命令
- `npm run dev` - 启动开发服务器
- `npm run build` - 构建生产版本
- `npm run test` - 运行测试
- `npm run lint` - 代码检查
````

最佳实践提示
在项目根目录创建 CLAUDE.md 文件
包含项目架构、编码规范和常用命令
定期更新以反映项目的最新状态
团队成员可以共享统一的 CLAUDE.md 配置

#### 工作流程策略

探索、规划、编码、提交工作流
这是最推荐的工作流程，帮助您系统化地处理编程任务。

探索
让 Claude Code 分析您的代码库，理解项目结构和现有实现。
> "请分析这个项目的架构，特别关注认证模块的实现"

规划 (Plan)
制定详细的实施计划，包括需要修改的文件和具体步骤。
> "基于现有架构，规划如何添加双因素认证功能"

编码 (Code)
执行计划，让 Claude Code 实现具体的代码更改。
> "按照计划实现双因素认证，包括前端界面和后端 API"

提交 (Commit)
审查更改并创建有意义的 Git 提交。
> "创建一个描述性的提交，说明添加的双因素认证功能"

#### 优化技巧

**具体明确的指令**
清晰、具体的指令能够大幅提高 Claude Code 的工作效率。
✅ 推荐
"在 src/components/User.tsx 中添加一个编辑按钮，点击后切换到编辑模式，使用现有的 Button 组件样式"
❌ 避免
"给用户资料添加编辑功能"

**善用视觉参考**
图片胜过千言万语，特别是在 UI 开发中。
使用设计稿作为实现参考
截图标注需要修改的部分
提供错误截图帮助调试
展示预期效果的参考图

**多实例协作**
使用 Git worktree 并行运行多个 Claude Code 实例。
一个实例处理前端，另一个处理后端
一个实例写代码，另一个写测试
一个实例重构，另一个添加新功能

**上下文管理**
定期清理上下文以保持最佳性能。
> /compact 保留用户认证相关的修改历史
💡 在完成大型任务后立即压缩上下文

**快速恢复最近对话**
交互式对话选择
> claude --resume
💡 使用箭头键导航并按Enter选择对话，您可以使用这个方法选择上下文

**通过 CLAUDE.md 存储重要记忆**
您可以使用以上命令设置一个CLAUDE.md文件来存储重要的项目信息、约定和常用命令
常用命令（构建、测试、lint）
记录代码风格偏好和命名约定
添加特定于您项目的重要架构模式
> /memory

#### 高级技巧

**自定义斜杠命令**
创建专属的命令来自动化常见任务。

```sh
# 在 ~/.claudecode/commands/ 目录下创建脚本
# deploy.sh
#!/bin/bash
echo "开始部署流程..."
npm run build
npm run test
git push origin main
echo "部署完成！"
```

**MCP 服务器集成**
通过模型上下文协议 (MCP) 扩展 Claude Code 的能力。
数据库连接
直接查询和修改数据库
API 集成
调用外部 API 服务
监控工具
获取系统性能指标

**子代理验证**
让 Claude Code 验证自己的工作，提高代码质量。
"实现用户注册功能后，请执行以下验证：\n1. 运行所有相关测试\n2. 检查代码是否符合项目规范\n3. 验证错误处理是否完善\n4. 确认没有安全漏洞\n5. 生成验证报告"

无头模式自动化
在 CI/CD 管道中使用 Claude Code。

```sh
name: AI Code Review
on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Claude Code
        run: npm install -g @anthropic-ai/claude-code
      - name: Run AI Review
        run: |
          claude -p "审查这个 PR 的代码变更，
          重点关注：
          1. 潜在的 bug
          2. 性能问题
          3. 安全隐患
          4. 代码风格一致性"
```

#### 安全考虑

**权限管理**
最小权限原则
仅启用必要的工具
定期审查权限设置
为不同项目使用不同配置
禁用生产环境的危险操作
提示：使用 /config 随时调整权限设置

**容器化隔离**
使用 Docker 隔离风险操作

```sh
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
# 限制容器权限
USER node
CMD ["claude"]
```

**代码审查**
审查 AI 生成的代码
总是审查提交前的更改
使用 git diff 仔细检查
运行测试验证功能
检查是否有敏感信息泄露

**备份策略**
保护您的工作
使用 Git 分支隔离实验性更改
定期提交工作进度
在重大更改前创建备份
使用 Git worktree 进行危险操作

#### 实用技巧集锦

**提高生产力**

- 批量操作
一次性描述多个相关任务，让 Claude Code 顺序完成
- 模板使用
在 CLAUDE.md 中定义常用的代码模板和模式
- 快捷记忆
使用 # 开头快速添加项目特定的记忆点

**调试技巧**
错误截图
提供错误截图能快速定位问题
日志分析
让 Claude Code 分析日志文件找出问题根源
增量调试
逐步添加调试语句，缩小问题范围

**沟通技巧**
上下文提供
说明您的最终目标，而不仅仅是当前步骤
示例驱动
提供期望输出的具体示例
迭代优化
通过多轮对话逐步完善结果

#### 常用模式

**重构模式**
> "分析 UserService 类，识别代码异味，提出重构建议并实施"

**性能优化模式**
> "分析页面加载性能，找出瓶颈，实施优化措施，并验证改进效果"

**文档生成模式**
> "为 API 模块生成完整的文档，包括使用示例和参数说明"

## OpenAI SDK

阿里云百炼官方提供了 Python 与 Java 编程语言的 SDK，也提供了与 OpenAI 兼容的调用方式（OpenAI 官方提供了 Python、Node.js、Java、Go 等 SDK）

### Node.js

```sh
npm install --save openai
```

### Python

```sh
pip install -U openai
```

### java

```xml
<dependency>
    <groupId>com.openai</groupId>
    <artifactId>openai-java</artifactId>
    <version>0.32.0</version>
</dependency>
```

### go

```sh
go get github.com/openai/openai-go@v0.1.0-alpha.62
```

## Cline

Cline 是一款基于 VSCode 的 AI 编程助手插件，原名为 Claude Dev。它集成了 Claude 3.5 Sonnet 模型，同时也支持其他模型，如 DeepSeek。其功能十分强大，涵盖代码补全、执行复杂任务、实时语法检查等。而且，Cline 是免费的，有望替代 GitHub Copilot，适用性广泛，甚至文科生也能轻松使用。

我个人感觉 Cline 和之前使用的编程工具最大的区别在于，它更像是一个智能体。当我们给它发送指令后，它会通过一系列思维链进行思考，然后再执行操作。这一点和 AutoGPT 以及之前很火的 Manus 类似。

比如，让其他编程智能体生成一段测试用例，通常需要先选中或复制程序代码，智能体分析代码后生成测试用例示例代码，接着创建测试文件，最后将代码拷贝进去。而 Cline 则能自动读取代码，并创建新文件将代码拷贝进去。

github地址： https://github.com/cline/cline

### Cline 功能概览

Cline作为VSCode的插件，为开发者提供了一系列强大的功能：

- 智能代码分析与生成
Cline能够分析项目的文件结构和源代码抽象语法树（AST）

通过正则表达式搜索和读取相关文件，快速了解现有项目

能够处理复杂的软件开发任务，逐步完成

- 文件操作与错误处理
可以创建和编辑文件

实时监控linter/编译器错误

能够主动修复诸如缺少导入和语法错误等问题

- 终端命令执行
直接在用户终端中执行命令并监控输出

能够对开发服务器问题等进行反应和处理

网页开发辅助
可以在无头浏览器中启动网站

捕获屏幕截图和控制台日志

帮助修复运行时错误和视觉bug

多模型支持
支持多种API提供商，如OpenRouter、Anthropic、OpenAI、Google Gemini等

可配置任何兼容OpenAI的API

支持通过Ollama使用本地模型

成本追踪
跟踪整个任务循环和单个请求的总token数和API使用成本

让用户随时了解开支情况

Cline的这些功能使其成为一个全面的编程助手，能够在项目开发的各个阶段为开发者提供支持。尤其是对OpenRouter的支持，对开发者是非常友好的。

Cline的使用方法和技术原理
安装和配置
安装：
在VSCode扩展市场搜索"Cline"并安装

或直接访问Cline (prev. Claude Dev) - Visual Studio Marketplace下载安装

配置：
选择API提供商（如OpenAI Compatible）

设置Base URL（如api.deepseek.com）

输入API Key

选择Model ID（如deepseek-coder）

可以在Custom Instructions中添加额外的prompts

建议勾选"Always allow read-only operations"以提高效率

技术原理
Cline的核心技术原理包括：

上下文管理：
通过仔细管理添加到上下文中的信息，Cline能够在不超出上下文窗口的情况下为大型复杂项目提供有价值的帮助
代码分析：
使用抽象语法树（AST）分析源代码结构

应用正则表达式进行代码搜索

人机交互：
提供人机交互GUI，让用户批准每个文件更改和终端命令

在保证安全的同时，探索代理AI的潜力

多模态技术：
支持图像分析（取决于使用的模型）

使用无头浏览器检查网站，捕获屏幕截图和控制台日志

Shell集成：
利用VSCode v1.93中的新shell集成更新，直接在终端中执行命令并接收输出
缓存机制：
实现输入Tokens的缓存命中，大幅降低API调用成本
通过这些技术，Cline能够深入理解项目结构，提供精准的代码建议和错误修复，同时保持高效的性能和较低的使用成本。

### Cline模型成本对比案例

为了更好地理解Cline的实际应用价值，我做了一个模型成本对比测试，分别用Claude 3.5 Sonnet和DeepSeek来实现网页版的扫雷游戏：

Claude 3.5 Sonnet 成本分析：
如下图所示，消耗47.7k输入tokens和4.2k输出tokens，花费$0.1299。

DeepSeek 成本分析：
如下图所示，消耗66.1k输入tokens和5.1k输出tokens，花费$0.0026，可是比Claude的模型便宜了不少啊。

所以现在无论是商用模型还是开源模型，Cline都能提供全面的支持，大大提高了开发效率。同时，开源模型DeepSeek以其低廉的使用成本也使得它成为开发者的另一个重要选择。不过从我测试的体验来看，DeepSeek的表现没有Claude那么丝滑，有时候可能不能一步到位，还需要用户进行错误的修正，而且DeepSeek不是多模态的，所以不能像Claude那样检查自己创造的作品，能力上相对有所限制。

Cline vs Other AI Coding Assistants

虽然市场上已有多种AI编程助手，但Cline在以下几个方面表现出独特的优势：

全面的项目支持
不仅提供代码补全，还能执行复杂的软件开发任务

从项目创建到文件编辑，再到终端命令执行，覆盖开发全流程

灵活的模型选择
支持多种API提供商和模型

可以根据需求和预算选择最适合的模型

成本效益高
特别是使用DeepSeek等模型时，成本显著降低

缓存机制进一步优化了token使用

人机协作
每一步操作都需要用户确认，保证了安全性

同时保持了AI自主性和人工控制的平衡

多模态能力
支持图像分析和网页检查

有助于解决视觉相关的开发问题

深度集成VSCode
作为VSCode插件，与开发环境紧密结合

利用VSCode的新特性（如shell集成）提供更强大的功能

相比之下，许多其他AI编程助手可能只专注于代码补全或简单的问题解答，而缺乏Cline这样全面的项目开发支持能力。

结论
Cline作为一款强大的VSCode插件，为开发者提供了全面的AI辅助编程解决方案。它不仅能够进行智能代码分析与生成，还能执行文件操作、终端命令，甚至协助网页开发。通过支持多种模型和API提供商，Cline为用户提供了灵活的选择，同时其高效的缓存机制和成本追踪功能也确保了使用的经济性。

从具体的应用案例中，我们可以看到Cline使用模型非常灵活。特别是在使用DeepSeek等模型时，Cline展现出极高的性价比，使得AI辅助编程变得更加经济实惠。

与其他AI编程助手相比，Cline的全面项目支持、灵活模型选择、高成本效益、人机协作模式以及多模态能力等特点，使其成为一个独特而强大的开发工具。它不仅能够提高开发效率，还能帮助开发者学习新技术，探索AI在软件开发中的潜力。

随着AI技术的不断进步，我们可以期待Cline在未来会有更多令人兴奋的功能和改进。对于希望提高编程效率、探索AI辅助开发的开发者来说，Cline无疑是一个值得尝试的强大工具。
