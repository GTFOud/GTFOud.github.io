---
functions:
  server:
    - description: Serve files in the local folder running an HTTP server. This requires PHP version 5.4 or later.
      code: |
        php -S $LHOST:$LPORT
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        php -r '$c=file_get_contents(getenv("$URL"));file_put_contents(getenv("$LFILE"), $c);'
---
