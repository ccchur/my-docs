---
type: canonical
status: accepted
category: preference
created: 2026-06-01
updated: 2026-06-01
tags: [agent, obsidian, workflow, memory]
reuse_scope: "所有需要读取或写入工程记忆的 agent 协作场景"
---

# Agent 协作规则

## 结论

工程记忆采用先入 inbox、人工审核、按需读取的流程。项目上下文留在项目内，Obsidian 只沉淀跨项目可复用的知识和偏好。

## 写入规则

- 不自动污染正式知识库。
- 可复用内容先进入 `inbox/`。
- 项目私有上下文、当前任务细节、临时代码决策留在项目仓库。
- 敏感信息不写入 `_agent-memory/`。
- 多个 agent 必须遵守同一套 Markdown 协议。

## 读取规则

- 读取工程记忆时，先读 `_agent-memory/README.md` 和 `_agent-memory/index.md`。
- 只读取与当前项目类型、技术栈、业务域或任务目标相关的笔记。
- 使用记忆影响计划或实现时，说明引用了哪些笔记。
- 如果笔记和当前项目事实冲突，以当前项目事实为准，并把冲突作为可复盘经验候选写入 inbox。

## 适用场景

- 跨项目继续开发时恢复个人偏好和协作规则。
- 让不同 agent 使用同一套工程记忆。
- 从一个项目萃取架构、技术栈、业务流程或调试经验。

## 不适用场景

- 保存某个项目的完整背景资料。
- 保存账号、密钥、客户隐私或商业敏感信息。
- 替代项目 README、架构文档或 issue 跟踪。