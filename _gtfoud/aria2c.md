---
description: Note that the subprocess is immediately sent to the background.
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request. Use `--allow-overwrite` if needed.
      code: |
        aria2c -o "$LFILE" "$URL"
---
