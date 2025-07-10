---
description: It serves files from a specified directory via HTTP, i.e., `http://<IP>:4444/x/<file>`.
functions:
  server:
    - code: |
        kubectl proxy --address=0.0.0.0 --port=$LPORT --www=$LFILE --www-prefix=/x/
---
