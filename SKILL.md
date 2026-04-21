---
name: qqbot-local-media
description: 将本机任意可读图片或文件复制到 OpenClaw 的本地媒体中转目录，供 QQBot 发送时使用。用于 QQBot 发送本地桌面文件、下载目录文件、工作区外文件失败时。优先在需要把本地绝对路径文件转成 QQBot 可接受路径时使用。
---

# QQBot Local Media

当用户要求把本机上的图片或文件发到 QQ，而直接发送原始路径失败时，使用这个 skill。

## 工作流

1. 运行脚本：`python scripts/stage_media.py <source_path>`
2. 脚本会把源文件复制到 `~/.openclaw/media/qqbot/` 下，并返回新的绝对路径
3. 对返回路径使用 QQBot 媒体标签：`<qqmedia>返回路径</qqmedia>`
4. 若文件超过 10MB，先明确告诉用户 QQBot skill 当前有大小限制

## 规则

- 只复制用户明确要求发送的文件
- 保留原扩展名
- 仅做复制，不修改原文件
- 如果源文件不存在，直接报错，不要猜测路径
- 如果要发送多个文件，逐个调用脚本并逐个输出 `<qqmedia>` 标签
