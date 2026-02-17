---
name: mdview
description: >
  Upload a markdown file to capshare.online and get a rendered view URL.
  Use when: "mdview README.md", "mdview docs/guide.md", or any request
  to share a rendered markdown file via capshare.
user_invocable: true
argument_description: "<filepath.md> - Path to the markdown file to upload and view"
---

# mdview

Upload a local markdown file to capshare.online's markdown viewer and return the shareable URL where it renders beautifully with GFM support (tables, task lists, code blocks).

## How It Works

1. Read the markdown file at the given path
2. Upload it via curl to `https://capshare.online/api/md/upload`
3. Return the `viewUrl` from the response - a link to the rendered markdown

## Execution

Given the argument `<filepath>`:

1. **Resolve the path**: If relative, resolve against the current working directory
2. **Upload and extract viewUrl in a single command** (no intermediate output shown to user):
   ```bash
   curl -sL -X POST -F "file=@<filepath>" https://capshare.online/api/md/upload | python3 -c "import sys,json; d=json.load(sys.stdin); print(d.get('viewUrl','ERROR: '+d.get('error','unknown')))"
   ```
3. **Present only the final URL** to the user - nothing else

## Response Format

On success, show ONLY:
```
<viewUrl>
```

Do NOT show the raw JSON, curl progress, or any other output. Keep it minimal.

## Notes

- The API accepts `.md`, `.markdown`, and `.txt` files
- Max file size: 50MB
- Files are stored on Vercel Blob storage
- The view URL renders markdown with GitHub Flavored Markdown support
- Alternative upload method (raw text): `curl -sL -X POST -H "Content-Type: text/plain" --data-binary @<file> https://capshare.online/api/md/upload`
