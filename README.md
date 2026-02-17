# mdview

A Claude Code skill that uploads markdown files to [capshare.online](https://capshare.online) and returns a shareable rendered URL.

## Installation

Copy or symlink this directory into your Claude Code skills folder:

```bash
# Option 1: Symlink (recommended - stays in sync with repo)
ln -s /path/to/mdview ~/.claude/skills/mdview

# Option 2: Copy
cp -r /path/to/mdview ~/.claude/skills/mdview
```

## Usage

In Claude Code, use the `/mdview` slash command followed by a file path:

```
/mdview README.md
/mdview docs/guide.md
/mdview ../notes/todo.md
```

Claude will upload the file and return a shareable URL where the markdown is rendered with GitHub Flavored Markdown support (tables, task lists, syntax-highlighted code blocks).

## Supported Files

- `.md`, `.markdown`, and `.txt` files
- Max file size: 50MB

## How It Works

1. Reads the markdown file at the given path
2. Uploads it to `https://capshare.online/api/md/upload`
3. Returns the rendered view URL
