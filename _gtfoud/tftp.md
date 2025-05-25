---
functions:
  file-upload:
    - description: Send local file to a TFTP server.
      code: |
        put $LFILE
  file-download:
    - description: Fetch a remote file from a TFTP server.
      code: |
        get $RFILE
---
