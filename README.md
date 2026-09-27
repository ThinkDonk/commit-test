# commit-test

基于 git 提交或工作区改动的选择性集成验证：分析影响面，准备环境，通过真实页面验证变更行为，分别保存模块知识与本次证据。P0 冒烟和变更验收分开记录，未覆盖的必要场景不会因已有提交基线而被跳过。

## 结构

```
SKILL.md          主干：流程、能力与授权边界（渐进加载）
phases/           细节：analysis（范围与影响）/ env（环境）/ execute（浏览器执行）
TEMPLATE.md       模块知识文件模板
projects/         本地积累区（git 忽略，不同步）
  └── <项目名>/
      ├── env.md             关联仓库、启动命令、地址、账号来源与环境限制
      ├── tested-commits.md  按 scope/depth/场景覆盖记录各仓库版本与相关 dirty
      ├── modules/*.md       稳定知识：触发范围、调用链、入口、场景与判断依据
      └── runs/*.md          每次验证的实际操作、结果、证据与未覆盖项
```

## 部署（本机链路）

本仓库为技能源目录，通过本机 junction 暴露给宿主：

```
D:\projects\CommonAssets\skills\commit-test          （源，git 同步）
  ├→ C:\Users\admin\.codex\skills\commit-test
  └→ C:\Users\admin\.config\opencode\skills\commit-test
       → C:\Users\admin\.zcode\skills\commit-test
```

## 同步语义

- **进 git**：SKILL.md、phases/、TEMPLATE.md 及现有 README（方法论，跨机器同步）
- **不进 git**：`projects/`（本机环境、基线、模块知识与运行证据；`.gitignore` 已排除）。忽略目录不等于凭据库，报告不复制密码/令牌。

换新机器拉取本仓库后，首次运行会现场初始化 `projects/<项目名>/`。

浏览器采用当前宿主实际可用的工具，不强制依赖特定辅助技能。详细执行、结果证据与基线更新规则见 [SKILL.md](SKILL.md) 及其阶段文档。
