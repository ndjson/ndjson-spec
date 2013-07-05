# LDJSON - Line delimited JSON

# Draft 1 (2013-07-05)

A standard for delimiting JSON in stream protocols (such as \[[TCP]\]).

## 1. Introduction

## 1.1 About

There is currently no standard for transporting JSON within a stream protocol, apart from \[[Websockets]\], which is unnecessarily complex for non-browser applications.

There were numerous possibilities for JSON framing, including counted strings and non-ASCII delimiters (DLE STX ETX or Websocket’s 0xFFs).

The primary use case for LDJSON is an unending stream of JSON objects, delivered at variable times, over TCP, where each object needs to be processed as it arrives. e.g. a stream of stock quotes or chat messages.

The specification must be:
* trivial to implement in multiple popular programming languages
* flexible enough to handle arbitrary whitespace (pretty-printed JSON)
* not contain non-printable characters
* netcat/telnet friendly

### 1.2 Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119. \[[RFC2119]\]

## 2. Example Output

(with \r\n line separators)

~~~~~
 {"some":"thing"}
 {"foo":17,"bar":false,"quux":true}
 {"may":{"include":"nested","objects":["and","arrays"]}}
~~~~~

## 3. Functional Specification

### 3.1 Sending

Each JSON object MUST be written to the stream followed by the carriage return and newline characters 0x0D0A. The JSON objects MAY contain newlines, carriage returns and any other permitted whitespace. See www.json.org for the full spec.

All serialized data MUST use the UTF8 encoding.

### 3.2 Receiving

The receiver SHOULD handle pretty-printed (multi-line) JSON.

The receiver MUST accept all common line endings: ‘0x0A’ (Unix), ‘0x0D’ (Mac OS), ‘0x0D0A’ (Windows).

#### 3.2.1 Trivial Implementation

A simple implementation is to accumulate received lines. Every time a line ending is encountered, an attempt MUST be made to parse the accumulated lines into a JSON object.

If the parsing of the accumulated lines is successful, the accumulated lines MUST be discarded and the parsed object given to the application code.

If the amount of unparsed, accumulated characters exceeds 16MiB the receiver MAY close the stream. Resource constrained devices MAY close the stream at a lower threshold, though they MUST accept at least 1KiB.

#### 3.2.2 Other Implementations

Alternate, more efficient, implementations are possible using a custom JSON parser.

The reference NodeJS/Javascript implementation can be found on github.

### 3.3 MIME Type and File Extensions

When using HTTP/email the MediaType \[[RFC4288]\] for Line Delimited JSON SHOULD be _application/x-ldjson_.

When saved in a file, the file extension SHOULD be _.ldjson_ or _.ldj_

## 4. Copyright

This specification is copyrighted by the authors named in section 4.1. It is free to use for any purposes commercial or non-commercial.

### 4.1 Authors

The following authors are responsible for the RestDoc core-specification:

~~~~
Thorsten Hoeger
Taimos GmbH
Hohenzollernstrasse 32
D-73262 Reichenbach
thorsten.hoeger@taimos.de
~~~~
~~~~
Chris Dew
~~~~
~~~~
Jim Wilson
~~~~

### 4.2 Contact

This specification and any related work is located at <https://github.com/ldjson>. 
Discussion and help can be found on the LDJSON Google group located at <https://groups.google.com/d/forum/ldjson>

## A. References

### A.1 Normative

[RFC2119]: http://www.ietf.org/rfc/rfc2119.txt "RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels"
\[RFC2119\]: RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels

[RFC4627]: http://www.ietf.org/rfc/rfc4627.txt "RFC 4627 - The application/json Media Type for JavaScript Object Notation (JSON)"
\[RFC4627\]: RFC 4627 - The application/json Media Type for JavaScript Object Notation (JSON)

[RFC4288]: http://www.ietf.org/rfc/rfc4288.txt "RFC 4288 - Media Type Specifications and Registration Procedures"
\[RFC4288\]: RFC 4288 - Media Type Specifications and Registration Procedures

[RFC2616]: http://www.ietf.org/rfc/rfc2616.txt "RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1"
\[RFC2616\]: RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1

### A.1 Informative

[TCP]: http://www.ietf.org/rfc/rfc793.txt "RFC 793 - Transmission Control Protocol"
\[TCP\]: RFC 793 - Transmission Control Protocol

[Websockets]: http://tools.ietf.org/html/rfc6455 "RFC 6455 - The WebSocket Protocol"
\[Websockets\]: RFC 6455 - The WebSocket Protocol
