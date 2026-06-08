# Vibe Coding GitHub 工作流 Skill

[English README](README.md)

本仓库用于建设一个依托 GitHub 的 vibe coding 多智能体开发流程标准化 skill，目前处于 WIP 初始骨架阶段。

这个 skill 的目标不是固化某个具体领域的 debug、研究文库维护或实现细节，而是固化一套通用协作协议：

- 先在 GitHub issue 中规划任务；
- 从上游 issue 或 umbrella PR 创建 empty PR；
- 让 PR body 具备足够强的计划性、可执行性和准出标准；
- 对较大任务拆 sub PR，并维护任务表与依赖图；
- 先发现本地可用 reviewer pool，再通过 GitHub comments 运行多 reviewer 的 C/I/M 分级 review；
- 迭代到 Critical / Important 问题全部关闭；
- 把 CI、测试和 Codecov comment 纳入 ready gate；
- 最终停在 ready-to-merge，等待 human maintainer 明确合并指示。

## 当前状态

本仓库现在只是初始骨架。第一个规划 issue 会定义实际 skill 范围、文件结构、模板、reviewer prompt 和验收门槛。在该 issue 被审阅并接受前，本仓库都应视为 WIP。

## 仓库结构

```text
.
├── README.md
├── README_zh.md
├── CLAUDE.md
├── AGENTS.md -> CLAUDE.md
├── SKILL.md
└── references/
    ├── comment-review-protocol.md
    ├── issue-planning-template.md
    ├── pr-body-template.md
    ├── readiness-checklist.md
    ├── reviewer-discovery.md
    ├── sub-pr-planning.md
    └── reviewer-prompt-template.md
```

`CLAUDE.md` 这个文件名用于兼容部分 agent 客户端的自动发现约定，内容本身不绑定 Claude；`AGENTS.md` 是指向同一内容的软链接，用于兼容偏好该约定的客户端。

## 计划建设的 Skill

该 skill 计划帮助一次 agentic / vibe coding 开发会话执行一套纪律化 GitHub 工作流：

1. 用 `gh` 读取上游 issue / PR 上下文。
2. 起草或审查 issue 计划。
3. 创建 contract-first 的 empty PR。
4. 从本地环境发现可用 reviewer agent 或外部 reviewer 进程。
5. 要求 reviewer 自行发布 GitHub comment。
6. 汇总 Critical / Important / Minor 问题。
7. 更新 issue 或 PR body，直到 C/I 清零。
8. 指导实现、CI watching、Codecov-aware review 和 ready-to-merge 汇报。

## 非目标

- 本仓库当前还不是成熟可复用 skill。
- 本仓库不固化具体 debug 或研究领域流程。
- 本仓库不自动决定 merge。
- 本仓库不默认 GitHub inline review 是主要审阅来源；issue / PR comments 是一等数据源。

## License

当前尚未选择许可证。正式对外复用前需要补充 license。
