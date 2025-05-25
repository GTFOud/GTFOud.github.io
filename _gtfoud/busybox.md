---
description: BusyBox may contain many UNIX utilities, run `busybox --list-full` to check what GTFOBins binaries are supported. Here some example.
functions:
  server:
    - description: Serve files in the local folder running an HTTP server.
      code: |
        busybox httpd -f -p $LPORT -h .
---
