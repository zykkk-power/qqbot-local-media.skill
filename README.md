# qqbot-local-media

A small OpenClaw skill for staging local files into the QQBot media relay directory so they can be sent through QQ more reliably.

## What it does

When a user wants to send a local desktop file, download, or any readable file outside the normal workspace, this skill copies the file into:

```text
~/.openclaw/media/qqbot/
```

Then the staged path can be sent with a QQBot media tag:

```xml
<qqmedia>/absolute/path/to/staged-file.ext</qqmedia>
```

## Use case

Use this skill when:

- QQBot needs to send a local file by path
- the original absolute path is outside the workspace
- direct sending fails because the file is not in a QQBot-friendly location
- a user asks to send a desktop/downloads file through QQ

## Repository contents

```text
qqbot-local-media/
├─ SKILL.md
├─ README.md
├─ .gitignore
└─ scripts/
   └─ stage_media.py
```

## How it works

1. Read `SKILL.md`
2. Run the staging script:

```bash
python scripts/stage_media.py <source_path>
```

3. The script copies the file to the OpenClaw QQBot media directory
4. It prints the staged absolute path
5. Send that path with `<qqmedia>...</qqmedia>`

## Script behavior

The script:

- verifies the source path exists
- only accepts a single file path argument
- enforces a 10 MB size limit
- preserves the original extension
- copies the file instead of modifying the original
- generates a UUID-based destination filename

## Example

```bash
python scripts/stage_media.py "C:\Users\zyk\Desktop\resume.pdf"
```

Example output:

```text
C:\Users\zyk\.openclaw\media\qqbot\9b0f3b80-19b2-410b-adfc-438d6028b93a.pdf
```

Then send:

```xml
<qqmedia>C:\Users\zyk\.openclaw\media\qqbot\9b0f3b80-19b2-410b-adfc-438d6028b93a.pdf</qqmedia>
```

## Notes

- Files larger than 10 MB are rejected
- The source file is never edited in place
- This repository stores the skill source, not the staged media output

## License

Add a license if you want to distribute or reuse the skill publicly.


# qqbot-local-media

一个小型的OpenClaw技能，用于将本地文件暂存到QQBot媒体中继目录，以便通过QQ更可靠地发送。

## 它的功能

当用户想要发送本地桌面文件、下载文件或任何可读文件到正常工作区之外时，此技能会将文件复制到：

~/.openclaw/media/qqbot/

然后可以通过QQBot媒体标签发送分阶段路径：

```xml
<qqmedia>/绝对/路径/到/暂存/文件.ext</qqmedia>
```

## 用例

在以下情况下使用此技能：

- QQBot 需要通过路径发送本地文件
- 原始绝对路径在工作区之外
- 直接发送失败，因为文件不在QQ Bot友好的位置 机器人友好的位置 
用户请求通过QQ发送桌面/下载文件。

## 仓库内容

qqbot-local-media/
├─ SKILL.md
├─ README.md
├─ .gitignore
└─ scripts/
   └─ stage_media.py

## 工作原理

1. 阅读 `SKILL.md`
2. 运行预发布脚本：

```bash
python scripts/stage_media.py <source_path>
```

3. 脚本将文件复制到 OpenClaw QQBot 媒体目录
4. 它打印出暂存的绝对路径
5. 发送带有 `<qqmedia>...</qqmedia>` 的路径

## 脚本行为

剧本：

- 验证源路径是否存在
- 只接受单个文件路径参数
- 强制限制文件大小为10 MB
- 保留原始扩展名
- 复制文件而不是修改原文件
- 生成一个基于UUID的目标文件名

## 示例

```bash
python scripts/stage_media.py  "C:\Users\zyk\Desktop\resume.pdf"

示例输出：

C:\Users\zyk\.openclaw\media\qqbot\9b0f3b80-19b2-410b-adfc-438d6028b93a.pdf

然后发送：

```xml
<qqmedia>C:\Users\zyk\.openclaw\media\qqbot\9b0f3b80-19b2-410b-adfc-438d6028b93a.pdf</qqmedia>
```

## 注释

- 大于10MB的文件会被拒绝
- 源文件从不在原地编辑
- 此存储库存储技能源代码，而不是暂存的媒体输出

## 许可证

如果您想公开分发或重用该技能，请添加许可证。



