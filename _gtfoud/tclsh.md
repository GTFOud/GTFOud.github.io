---
functions:
  server:
    - description: |
        Serve files in the local folder running an HTTP server.
        Add the code snippet into a TCL file, before running it using: `tclsh script.tcl`
      code: |
        proc handler {sock addr port} {
            fconfigure $sock -translation binary -buffering none

            gets $sock line
            puts "REQUEST: $line"

            # Parse requested file
            if {[regexp {^GET /([^ ]*) HTTP} $line -> file]} {
                set file [string trim $file "/"]
            } else {
                puts $sock "HTTP/1.1 400 Bad Request\r\n\r\n"
                close $sock
                return
            }

            # Send file if it exists
            if {[file exists $file]} {
                set f [open $file r]
                fconfigure $f -translation binary
                set data [read $f]
                close $f

                set size [string bytelength $data]

                puts -nonewline $sock "HTTP/1.1 200 OK\r\n"
                puts -nonewline $sock "Content-Type: application/octet-stream\r\n"
                puts -nonewline $sock "Content-Length: $size\r\n"
                puts -nonewline $sock "Connection: close\r\n\r\n"
                puts -nonewline $sock $data
            } else {
                puts -nonewline $sock "HTTP/1.1 404 Not Found\r\nContent-Length: 13\r\n\r\nFile not found"
            }

            flush $sock
            close $sock
        }

        socket -server handler 4444
        puts "Tcl HTTP server running on port 4444..."
        vwait forever
---
