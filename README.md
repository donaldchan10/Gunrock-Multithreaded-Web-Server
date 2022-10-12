# Gunrock Web Server
This web server is a simple server used in ECS 150 for teaching about multi-threaded programming and operating systems. This version of the server can only handle one client at a time and simply serves static files. Also, it will close each connection after reading the request and responding, but generally is still HTTP 1.1 compliant.

This server was written by Sam King from UC Davis and is actively maintained by Sam as well. The `http_parse.c` file was written by [Ryan Dahl](https://github.com/ry) and is licensed under the BSD license by Ryan. This programming assignment is from the [OSTEP](http://ostep.org) textbook (tip of the hat to the authors for writing an amazing textbook).

# Quickstart
To compile and run the server, open a terminal and execute the following commands:
```bash
$ git clone https://github.com/kingst/gunrock_web.git
$ cd gunrock_web
$ make
$ ./gunrock_web
```

To test it out, you can either open up a web browser on the same machine and give it this url `http://localhost:8080/hello_world.html` or if you want to use curl on the command line you can test it out like this:
```bash
$ # get a basic HTML file
$ curl http://localhost:8080/hello_world.html
$ # get a basic HTML file with more detailed information
$ curl -v http://localhost:8080/hello_world.html
$ # head a basic HTML file
$ curl --head http://localhost:8080/hello_world.html
$ # test out a file that does not exist (404 status code)
$ curl -v http://localhost:8080/hello_world2.html
$ # test out a POST, which isn't supported currently (405 status code)
$ curl -v -X POST http://localhost:8080/hello_world.html
```

We also included a full website that you can use for testing, try pointing your browser to: `http://localhost:8080/bootstrap.html`

# Gunrock internals

## Other files
- **gunrock** - The main function + basic request handling
- **FileService** - Main file service, where the application logic for reading files goes
- **dthread** -- The main threading utilities, use the functions in this file for your threads
- **HTTP** - Higher level HTTP object, interfaces with the `http_parser`
- **http_parser** - HTTP protocol parsing state machine and callback functionality
- **HTTPRequest** - The HTTP request object, this is filled in by the framework
- **HTTPResponse** - The HTTP response object, the data for the response is filled in by the service
- **HttpUtils** - Simple utility functions for working with HTTP data
- **MyServerSocket** - High level abstraction on top of server sockets, accepts connections from new clients
- **MySocket** - High level abstraction on top of sockets, used by the framework to read requests and write responses


