---
description: This tool is installed starting with Java SE 6.
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        jrunscript -e "cp('$URL','$LFILE')"
---
