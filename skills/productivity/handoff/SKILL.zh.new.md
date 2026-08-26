---
name: handoff
description: 把当前对话压缩成一份交接文档，供另一个 agent 接着工作。
argument-hint: "下一个会话要用来做什么？"
disable-model-invocation: true
---

把当前对话榨成一份交接文档，让一个新 agent 打开就能接着干。存到用户操作系统的临时目录，别往当前工作区里塞。

文档里加一个"建议 skill"章节，列清楚下一个 agent 该用 Skill 工具召唤哪些 skill。

已经写进别的地方的东西（规格、计划、ADR、issue、commit、diff）别在文档里再抄一遍，用路径或 URL 指过去就行。

敏感信息一律脱敏：API 密钥、密码、能认出是谁的信息，统统抹掉。

用户要是传了参数，就当它是下个会话要干什么的说明，照着调整文档。