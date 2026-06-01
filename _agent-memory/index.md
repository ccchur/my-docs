# 工程记忆索引

这是 `_agent-memory/` 的入口。新的 agent 在读取工程记忆时，应先读 `README.md`，再按当前项目相关性读取下面的分类。

## 入口

- [使用协议](README.md)
- [待审核收件箱](inbox/README.md)
- [摘录模板](templates/inbox-capture.md)
- [正式笔记模板](templates/canonical-note.md)

## 分类

- [架构模式](architecture/)
- [技术栈经验](tech-stacks/)
- [业务流程](business-flows/)
- [经验教训](lessons/)
- [个人偏好与 AI 设置](preferences/)

## 当前已确认偏好

- [Agent 协作规则](preferences/agent-collaboration.md)

## 维护方式

- inbox 中的候选摘录经过用户确认后，再移动到正式分类。
- 正式笔记应该保持短小、可复用、可链接。
- 当某条经验失效时，更新原笔记的 `updated` 字段并说明变化，不保留过期结论作为默认规则。