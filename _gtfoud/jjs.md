---
description: This tool is installed starting with Java SE 8.
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        echo "var URL = Java.type('java.net.URL');
        var ws = new URL('$URL');
        var Channels = Java.type('java.nio.channels.Channels');
        var rbc = Channels.newChannel(ws.openStream());
        var FileOutputStream = Java.type('java.io.FileOutputStream');
        var fos = new FileOutputStream('$LFILE');
        fos.getChannel().transferFrom(rbc, 0, Number.MAX_VALUE);
        fos.close();
        rbc.close();" | jjs
---
