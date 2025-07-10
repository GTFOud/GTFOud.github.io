---
functions:
  file-upload:
    - description: Send local file to a SSH server.
      code: |
        scp $LFILE $RPATH
  file-download:
    - description: Fetch a remote file from a SSH server.
      code: |
        scp $RPATH $LFILE
---
