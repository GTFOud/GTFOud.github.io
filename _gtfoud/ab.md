---
functions:
  file-upload:
    - description: Upload local file via HTTP POST request.
      code: |
        ab -p $LFILE $URL
  file-download:
    - description: Fetch a remote file via HTTP GET request. The response is returned as part of the verbose output of the program with some limitations on the length.
      code: |
        ab -v2 $URL
---
