---
description: sendmail differs between systems, depending on whether it is postfix, exim, or otherwise, which provides the binary.
functions:
  file-upload:
    - description: Arbitrary files can be delivered.
      code: |
        sendmail -t -i -f mail@address.com -C$LFILE -X/dev/null < mail.txt
---
