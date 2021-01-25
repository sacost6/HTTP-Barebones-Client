## HTTP-Barebones-Client

# A Barebones HTTP/1.1 Client

In this programming exercise, you will create a barebones web client. While
python includes a basic http client module `http.client`, this assignment will
serve as a learning experience for translating a protocol into an
implementation. Your deliverable will be a client which only implements the
`GET` method and follows the basics of the HTTP/1.1 specification, enough to
download files as one would with the command line program `curl`. In addition to 
this you are also required to verify the certificate of pages that you connect
https.

# HTTP/1.1 Features

[HTTP/1.0](https://tools.ietf.org/search/rfc1945) describes the most basic
functionality that an HTTP client is required to do. HTTP/1.1 includes several
new features that extend the protocol. For this assignment, you will only be
required to implement these additional features:

  * Include a `Host:` header
  * Correctly interpret `Transfer-encoding: chunked`
  * Include a `Connection: close` header, or handle persistent connections

These new features are described in James Marshall's excellent [HTTP Made Really Easy](https://www.jmarshall.com/easy/http/#http1.1clients) under the HTTP/1.1
clients subsection.

Note that the RFCs are your friends: if you're having trouble with
`Transfer-encoding`, check [the RFC][http] for hints!


# Basic HTTP functionality

As seen in class, HTTP is a stateless request-response protocol that consists
of an initial line, zero or more headers, and zero or more bytes of content.
Your program will implement a function, `retrieve_url`, which takes a url (as
a `str`) as its only argument, and uses the HTTP protocol to retrieve and
return the body's bytes (do not decode those bytes into a string). Consult
the book or your class notes for the basics of the HTTP protocol.

You may assume that the URL will not include a fragment, query string, or
authentication credentials. You are not required to follow any redirects -
only return bytes when receiving a `200 OK` response from the server. If for
any reason your program cannot retrieve the resource correctly, `retrieve_url`
should return `None`.

# Validating HTTPS
Within the `retrieve_url` you will also be required to ensure that when connecting
to a HTTPS based website, your client ensures a valid certificate is provided by the server. The `ssl` library in Python will do this for you by default.
If the returned certificate is invalid (expired, wrong host etc) and cannot be validated `retrieve_url` returns `None`. To test your code in addition to the provided tests, there are examples available at [badssl.com](https://badssl.com/).
