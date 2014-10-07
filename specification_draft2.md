# NDJSON - Newline delimited JSON

# Draft 2 (2014-09-25)

A standard for delimiting JSON in stream protocols.

## 1. Introduction

## 1.1 About

There is currently no standard for transporting instances of JSON text within a stream protocol, apart from \[[Websockets]\], which is unnecessarily complex for non-browser applications.

A common use case for NDJSON is delivering multiple instances of JSON text through streaming protocols like TCP or UNIX Pipes. It can also be used to
store semi-structured data.


### 1.2 Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119. \[[RFC2119]\]

## 2. Example NDJSON

~~~~~
 {"some":"thing"}
 {"foo":17,"bar":false,"quux":true}
 {"may":{"include":"nested","objects":["and","arrays"]}}
~~~~~
(with `\n` line separators)

## 3. Functional Specification

### 3.1 Serialization

Each JSON text MUST conform to the \[[RFC7159]\] standard and MUST be written to the stream followed by the newline character `\n` (0x0A). The newline charater MAY be preceeded by a carriage return `\r` (0x0D). The JSON texts MUST NOT contain newlines or carriage returns.

All serialized data MUST use the UTF8 encoding.

### 3.2 Parsing

The parser MUST accept newline as line delimiter `\n` (0x0A) as well as carriage return and newline `\r\n` (0x0D0A). 

If the JSON text is not parseable, the parser SHOULD raise an error. However, the parser MAY silently ignore empty lines, e.g. `\n\n`. This behavior 
MUST be documented and SHOULD be configurable by the user of the parser.

### 3.3 MIME Type and File Extensions

The MediaType \[[RFC4288]\] for Newline Delimited JSON SHOULD be _application/x-ndjson_.

When saved in a file, the file extension SHOULD be _.ndjson_.

## 4. Copyright

This specification is copyrighted by the authors named in section 4.1. It is free to use for any purposes commercial or non-commercial.

### 4.1 Authors

The following authors are responsible for the NDJSON core-specification:

~~~~
Thorsten Hoeger
Taimos GmbH
Hohenzollernstrasse 32
D-73262 Reichenbach
thorsten.hoeger@taimos.de
~~~~
~~~~
Chris Dew
chris.dew@barricane.com
~~~~
~~~~
Finn Pauls
ich@finnpauls.de
~~~~
~~~~
Jim Wilson
~~~~

### 4.2 Contact

This specification and any related work is located at <https://github.com/ndjson>. 
Discussion and help can be found on the issues page.

## A. References

### A.1 Normative

[RFC2119]: http://www.ietf.org/rfc/rfc2119.txt "RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels"
\[RFC2119\]: RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels

[RFC7159]: http://www.ietf.org/rfc/rfc7159.txt "RFC 7159 -  The JavaScript Object Notation (JSON) Data Interchange Format"
\[RFC7159\]: RFC 7159 -  The JavaScript Object Notation (JSON) Data Interchange Format

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
