---
functions:
  file-upload:
    - description: Send local file to a FTP server.
      code: |
        ftp $RHOST
        put $FILE
  file-download:
    - description: Fetch a remote file from a FTP server.
      code: |
        ftp $RHOST
        get $FILE
---
