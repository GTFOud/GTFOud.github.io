---
functions:
  file-upload:
    - description: Send local file to a SSH server.
      code: |
        sftp $RHOST
        put $LFILE $RFILE
  file-download:
    - description: Fetch a remote file from a SSH server.
      code: |
        sftp $RHOST
        get $RFILE $LFILE
---
