---
name: handoff
description: 把当前对话压缩成一份交接文档，供另一个 agent 接着工作。
argument-hint: "下一个会话要用来做什么？"
disable-model-invocation: true
---

写一份交接文档，总结当前对话，让一个全新的 agent 能继续工作。保存到用户操作系统的临时目录，而不是当前工作区。

在文档里包含一个"建议 skill"章节，列出下一个 agent 应该用 Skill 工具调用哪些 skill。

不要重复已经被其他产物（规格、计划、ADR、issue、commit、diff）捕获的内容。改为用路径或 URL 引用它们。

脱敏任何敏感信息，比如 API 密钥、密码或可识别个人身份的信息。

如果用户传了参数，把它当作对下一个会话内容的描述，并据此调整文档。