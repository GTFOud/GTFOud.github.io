---
functions:
  server:
    - description: Serve files in the local folder running an HTTP server.
      code: |
        irb
        require 'webrick'; WEBrick::HTTPServer.new(:Port => $LPORT, :DocumentRoot => Dir.pwd).start;
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        irb
        require 'open-uri'; download = open(ENV['$URL']); IO.copy_stream(download, ENV['$LFILE'])
---
