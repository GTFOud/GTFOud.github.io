---
layout: page
title: Contribute
---

## Structure

Each GTFO binary is defined in a file in the [`_gtfoud/`] folder named as `<binary name>.md`, such file consists only of a [YAML] front matter which describes the binary and its functions.

The full syntax is the following:

```
---
description: Optional description of the binary
functions:
  FUNCTION:
    - description: Optional description of the example
      code: Code of the example
    - ....
  FUNCTION:
    - description: Optional description of the example
      code: Code of the example
    - ...
  ...
---
```

Where `FUNCTION` is one of the values described in the [`_data/functions.yml`] file.

Feel free to use any file in the [`_gtfoud/`] folder as an example.

## GTFOud Pull request process

Before sending a PR, ensure the following:

1. **Platform Compatibility**

   - Confirm that the technique works on at least one modern **Unix** or **Windows** system (e.g., Kali, Ubuntu, Windows 10+)
   - Specify the **platform(s)** in the metadata (`platform: Unix`, `Windows`, or `Cross-platform`)

2. **Function Type Classification**

   - Label the technique correctly as one or more of the following:
     - `server`: It can act as a server to host or receive files.
     - `file-upload`: It can exfiltrate local files to a remote host.
     - `file-download`: It can download remote files to the local system.
     - `data-transfer`: It can transmit command/file output or encoded data.
     - `chaining`: Combine multiple techniques or actions sequentially to GTFO.
   - If the tool supports multiple actions, include all applicable tags.

3. **One-liner or Simple Code Snippet**

   - Include a functional **one-liner** or **minimal script** (e.g., `curl`, `powershell`, `python`, etc...)
   - Avoid using 3rd-party tools unless commonly pre-installed (e.g., `busybox`, `ftp`, `tftp`)

4. **Native / Living-off-the-land Usage**

   - The tool must be **commonly present** on the system or **natively usable** without requiring installation.
   - Avoid tools that require external access to the internet: `pip install`, `npm install`, `apt install`, etc...

5. **Dependencies & Requirements**

   - Clearly state any required service (e.g., TFTP server), arguments, or default behaviors (e.g., passive FTP)
   - Specify if it only works with certain shell types, OS builds, or tool versions.

6. **Test Before Submitting**

   - Run and validate your command(s) in a local lab environment or VM.
   - If submitting a new tool, also provide metadata (`_gtfoud/<tool>.md` and `_data/functions.yml` entry)

7. **Documentation**
   - Add a short description and any relevant **caveats** (e.g., firewall requirements, OS-specific quirks)
   - Provide usage context where possible (e.g., “bypasses upload restrictions by abusing...”)

Need help classifying your tool or writing clean metadata?  
Check our example files in `_gtfoud/` and `_data/functions.yml`.

Pull requests adding new functions in [`_data/functions.yml`] are allowed and subjected to project maintainers vetting.

[YAML]: https://yaml.org/
[`_gtfoud/`]: https://github.com/GTFOud/GTFOud.github.io/tree/main/_gtfoud
[`_data/functions.yml`]: https://github.com/GTFOud/GTFOud.github.io/blob/main/_data/functions.yml
