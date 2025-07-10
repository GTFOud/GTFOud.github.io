---
functions:
  file-upload:
    - description: Send local file to a SSH server.
      code: |
        ssh $RHOST "cat > $NFILE" < $LFILE
  file-download:
    - description: Fetch a remote file from a SSH server.
      code: |
        ssh $RHOST "cat $NFILE" > $LFILE
---
