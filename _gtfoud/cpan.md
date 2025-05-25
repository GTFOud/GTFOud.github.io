---
functions:
  server:
    - description: Serve files in the local folder running an HTTP server on port 8080. Install the dependency via `cpan HTTP::Server::Simple`.
      code: |
        cpan
        ! use HTTP::Server::Simple; my $server= HTTP::Server::Simple->new(); $server->run();
  file-download:
    - description: Fetch a remote file via an HTTP GET request and store it in `PWD`.
      code: |
        cpan
        ! use File::Fetch; my $file = (File::Fetch->new(uri => "$ENV{$URL}"))->fetch();
---
