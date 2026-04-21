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
