# git 工作流

> Git 的分支就像“平行宇宙”，每个分支代表代码的不同版本。团队通过分支协作，避免互相干扰。

在 Git 中，分支的建立顺序通常遵循 Git Flow 或 GitHub Flow 等标准工作流。

以下是基于 Git Flow 的标准分支管理顺序和操作流程：

## Git Flow

### 主分支（Main/Master）

- 作用：存储生产环境代码，始终稳定，禁止直接开发。
- 创建时机：项目初始化时默认存在（通常命名为 `main` 或 `master`）。
- 操作规范：
  - 仅通过合并 `release` 或 `hotfix` 分支更新。
  - 合并后需打标签（如 `v1.0.0`）标记版本。

### 开发分支（Develop）

- 作用：集成所有新功能和修复的主分支，作为开发的基线。
- 创建顺序：从主分支 `main` 创建。
- 操作流程

```sh
# 从 main 创建 develop 分支
git checkout main
git checkout -b develop
git push -u origin develop
```

- 注意事项：
  - 所有功能分支（`feature/*`）和修复分支（`bugfix/*`）应基于 `develop` 创建。
  - 禁止直接在 `develop` 上开发，需创建子分支。

### 功能分支（Feature Branches）

- 作用：开发新功能或实现需求。
- 命名规范：`feature/<功能描述>`（如 `feature/user-auth`）。
- 创建顺序：从 `develop` 创建。
- 操作流程：

```sh
# 切换到 develop 并拉取最新代码
git checkout develop
git pull origin develop

# 创建并切换到功能分支
git checkout -b feature/user-auth
git push -u origin feature/user-auth
```

- 生命周期：
  - 完成开发后合并回 `develop`。
  - 合并后删除分支（`git branch -d feature/user-auth`）。

### 发布分支（Release Branches）

- 作用：准备版本发布，修复非紧急问题。
- 命名规范：`release/<版本号>`（如 `release/1.0.0`）。
创建顺序：从 `develop` 创建。
操作流程：

```sh
# 创建 release 分支
git checkout develop
git checkout -b release/1.0.0
git push -u origin release/1.0.0

# 测试并修复问题
git commit -am "Fix bug in release"

# 合并到 main 和 develop
git checkout main
git merge release/1.0.0
git tag v1.0.0  # 打标签

git checkout develop
git merge release/1.0.0

# 删除 release 分支
git branch -d release/1.0.0
```

### 紧急修复分支（Hotfix Branches）

- 作用：修复线上紧急问题。
- 命名规范：`hotfix/<问题描述>`（如 `hotfix/login-error`）。
- 创建顺序：从 `main` 创建。
- 操作流程：

```sh
# 创建 hotfix 分支
git checkout main
git checkout -b hotfix/login-error
git push -u origin hotfix/login-error

# 修复问题并提交
git commit -am "Fix login error"

# 合并到 main 和 develop
git checkout main
git merge hotfix/login-error
git tag v1.0.1  # 打标签

git checkout develop
git merge hotfix/login-error

# 删除 hotfix 分支
git branch -d hotfix/login-error
```

### 其他分支（Bugfix/实验性分支）

- 作用：修复小问题或尝试实验性功能。
- 命名规范：`bugfix/<问题描述>` 或 `experiment/<功能描述>`。
- 创建顺序：根据需求从 `develop` 或特定分支创建。

### 常见错误与注意事项

1. 不要直接在 `main` 或 `develop` 上开发：
功能分支应基于 `develop`，修复分支应基于 `main`。

2. 分支命名规范：
使用统一前缀（如 `feature/`、`hotfix/`）便于识别用途。

3. 推送分支时设置上游：

```sh
git push -u origin <branch-name>  # 首次推送时绑定远程分支
```

1. 合并前拉取最新代码：

```sh
git pull origin develop  # 合并到 develop 前确保同步
```

### 分支管理示意图

```sh
main/master      --- (1) Hotfix 分支合并后打标签
       \
        \--- develop (2) 功能分支合并后更新
               \
                \--- feature/user-auth (3) 新功能开发
                \--- release/1.0.0 (4) 发布准备
                \--- hotfix/login-error (5) 紧急修复
```

### 总结

- 标准顺序：`main` → `develop` → `feature/*` → `release/*` → `hotfix/*`。
- 核心原则：
  - 功能开发在 `feature` 分支，集成到 `develop`。
  - 发布准备在 `release` 分支，最终合并到 `main`。
  - 紧急问题在 `hotfix` 分支，合并到 `main` 和 `develop`。

## 实际操作步骤（新手版）

### 场景 1：开发新功能

从 develop 分支创建新分支：

```sh
git checkout develop       # 切换到 develop 分支
git checkout -b feature/user-login  # 创建 feature 分支
```

开发完成后合并回 develop：

```sh
git checkout develop       # 回到 develop 分支
git merge feature/user-login  # 合并 feature 分支
git branch -d feature/user-login  # 删除 feature 分支
```

### 场景 2：发布版本

从 develop 创建 release 分支：

```sh
git checkout develop
git checkout -b release/v1.0.0
```

修复 bug 并合并到 main 和 develop：

```sh
git checkout main
git merge release/v1.0.0  # 合并到 main
git tag v1.0.0            # 打标签
git checkout develop
git merge release/v1.0.0  # 合并到 develop
git branch -d release/v1.0.0  # 删除 release 分支
```

### 场景 3：紧急修复线上问题

从 main 创建 hotfix 分支：

```sh
git checkout main
git checkout -b hotfix/login-bug
```

修复后合并到 main 和 develop：

```sh
git checkout main
git merge hotfix/login-bug  # 合并到 main
git checkout develop
git merge hotfix/login-bug  # 合并到 develop
git branch -d hotfix/login-bug  # 删除 hotfix 分支
```

## 常见问题解答

Q1：分支命名有什么规范？

- `feature/功能名称`（如 `feature/add-cart`）
- `release/版本号`（如 `release/v1.0.0`）
- `hotfix/问题描述`（如 `hotfix/login-error`）

Q2：合并时出现冲突怎么办？

- 冲突是因为同一文件被不同分支修改了。
- 解决方法：
  1. 使用 `git merge` 后，Git 会标记冲突的文件。
  2. 手动编辑文件，保留需要的代码。
  3. 用 `git add` 标记冲突已解决。
  4. 最后 `git commit` 完成合并。

Q3：分支用完后需要删除吗？

- 是的！完成任务后删除分支（如 `feature`、`release`、`hotfix`），保持仓库整洁。

### 分支总结

- Git Flow的主要分支

  - 主分支（Master）：存放最稳定的正式版本代码，任何时候都可以在生产环境中使用。

  - 开发分支（Develop）：包含所有即将发布的新功能，是日常开发的主要分支。

- Git Flow的辅助分支

  - 功能分支（Feature）：用于开发新功能，基于Develop分支创建，开发完成后合并回Develop分支。

  - 预发分支（Release）：用于准备发布版本，允许进行小量级的Bug修复和元数据更新。

  - 热修复分支（Hotfix）：用于紧急修复生产环境中的严重缺陷，基于Master分支创建。

### Git Flow的工作流程

- 创建Develop分支

```sh
git branch develop
git push -u origin develop
```

- 开始新的Feature

```sh
git checkout -b feature/分支名 develop
git push -u origin feature/分支名

```

- 完成Feature分支

```sh
git pull origin develop
git checkout develop
git merge --no-ff feature/分支名
git push origin develop
git branch -d feature/分支名
```

- 开始Release

```sh
git checkout -b release/版本号 develop

```

- 完成Release

```sh
git checkout master
git merge --no-ff release/版本号
git push
git checkout develop
git merge --no-ff release/版本号
git push
git branch -d release/版本号
```

- 开始Hotfix

```sh
git checkout -b hotfix/版本号 master
```

- 完成Hotfix

```sh
git checkout master
git merge --no-ff hotfix/版本号
git push
git checkout develop
git merge --no-ff hotfix/版本号
git push
git branch -d hotfix/版本号
git tag -a v版本号 master
git push --tags
```

### proxy代理

```sh
git config --global http.proxy 'http://127.0.0.1:10808'
git config --global https.proxy 'https://127.0.0.1:10808'

git config --global --unset http.proxy
git config --global --unset https.proxy

git config http.proxy http://127.0.0.1:10808
git config https.proxy https://127.0.0.1:10808

git config --unset http.proxy
git config --unset https.proxy
```

### git 登录 github

```sh
# 首次
ssh-keygen -t ed25519 -C "lixiwang@126.com"

more C:\Users\lixiwang\.ssh\id_rsa.pub
# Settings -> SSH keys -> New SSH key
ssh -T git@github.com
git config --global url."git@github.com:".insteadOf "https://github.com/"
```
