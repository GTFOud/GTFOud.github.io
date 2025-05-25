---
description: Fetch a remote file via HTTP GET request.
functions:
  file-download:
    - code: |
        lwp-download $URL $LFILE
---
