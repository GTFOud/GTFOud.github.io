---
description: HTTPie is a command-line HTTP client designed for human-friendly interaction with web services. It supports file uploads, downloads, and JSON-friendly syntax.
functions:
  file-download:
    - description: Download a file from a remote server using HTTP GET with the `--download` flag.
      code: |
        http http://$RHOST:$RPORT/$RFILE --download
  file-upload:
    - description: Upload a file via HTTP POST using `httpie` form-encoded upload.  Server must support POST requests (e.g., with an appropriate upload handler).
      code: |
        http -f POST http://$RHOST:$RPORT/upload files@$LFILE
---
