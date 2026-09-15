# commit-test

基于 git 提交记录的**选择性集成测试**编排 skill：分析提交改动 → 识别受影响功能模块 → 启动前后端 → 浏览器走通主流程 → 探索结果沉淀为项目知识，下次复用。

## 结构

```
SKILL.md          主干：流程 + 铁律（渐进加载/沉淀/自愈/基线）
phases/           细节：analysis（范围与影响）/ env（环境）/ execute（浏览器执行）
TEMPLATE.md       模块知识文件模板
projects/         本地积累区（git 忽略，不同步）
  └── <项目名>/
      ├── env.md             启动命令、端口、健康检查、账号
      ├── tested-commits.md  已验证基线，下次默认增量
      └── modules/*.md       模块知识：触发范围、页面入口、主流程步骤
```

## 部署（本机链路）

源在本仓库 `skills/commit-test`，通过两级 junction 暴露给各 agent CLI：

```
D:\projects\CommonAssets\skills\commit-test          （源，git 同步）
  → C:\Users\admin\.config\opencode\skills\commit-test
  → C:\Users\admin\.zcode\skills\commit-test
```

## 同步语义

- **进 git**：SKILL.md、phases/、TEMPLATE.md（方法论，跨机器同步）
- **不进 git**：`projects/`（每台机器自己的积累：账号、基线、模块知识——`commit-test/.gitignore` 已排除）

换新机器拉取本仓库后，首次运行会现场初始化 `projects/<项目名>/`。
