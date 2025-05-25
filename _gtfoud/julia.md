---
functions:
  file-download:
    - code: |
        julia -e 'download(ENV["$URL"], ENV["$LFILE"])'
---
