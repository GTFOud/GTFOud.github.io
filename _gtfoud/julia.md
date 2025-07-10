---
functions:
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        julia -e 'download(ENV["$URL"], ENV["$LFILE"])'
---
