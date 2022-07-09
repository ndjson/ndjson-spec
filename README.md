---
title: NDJSON - Newline delimited JSON
version: 1.0.0
last_update: 2014-10-19
created: 2013-07-05
---

# NDJSON - Newline delimited JSON

A standard for delimiting JSON in stream protocols.

## 1. Introduction

## 1.1 About

There is currently no standard for transporting instances of JSON text within a stream protocol, apart from \[[Websockets]\], which is unnecessarily complex for non-browser applications.

A common use case for NDJSON is delivering multiple instances of JSON text through streaming protocols like TCP or UNIX Pipes. It can also be used to store semi-structured data.

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

Each JSON text MUST conform to the \[[RFC8259]\] standard and MUST be written to the stream followed by the newline character `\n` (0x0A). The newline character MAY be preceded by a carriage return `\r` (0x0D). The JSON texts MUST NOT contain newlines or carriage returns.

All serialized data MUST use the UTF8 encoding.

### 3.2 Parsing

The parser MUST accept newline as line delimiter `\n` (0x0A) as well as carriage return and newline `\r\n` (0x0D0A). 

If the JSON text is not parsable, the parser SHOULD raise an error. The parser MAY silently ignore empty lines, e.g. `\n\n`. This behavior MUST be documented and SHOULD be configurable by the user of the parser.

### 3.3 MediaType and File Extensions

The MediaType \[[RFC6838]\] for Newline Delimited JSON SHOULD be _application/x-ndjson_.

When saved to a file, the file extension SHOULD be _.ndjson_.

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
Discussion and help is located at <https://github.com/ndjson/ndjson-spec/issues>. 

## A. References

### A.1 Normative

[RFC2119]: https://tools.ietf.org/html/rfc2119 "RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels"
\[[RFC2119]\]: RFC 2119 - Key words for use in RFCs to Indicate Requirement Levels

[RFC8259]: https://tools.ietf.org/html/rfc8259 "RFC 8259 -  The JavaScript Object Notation (JSON) Data Interchange Format"
\[[RFC8259]\]: RFC 8259 -  The JavaScript Object Notation (JSON) Data Interchange Format

[RFC4627]: https://tools.ietf.org/html/rfc4627 "RFC 4627 - The application/json Media Type for JavaScript Object Notation (JSON)"
\[[RFC4627]\]: RFC 4627 - The application/json Media Type for JavaScript Object Notation (JSON)

[RFC6838]: https://tools.ietf.org/html/rfc6838 "RFC 6838 - Media Type Specifications and Registration Procedures"
\[[RFC6838]\]: RFC 6838 - Media Type Specifications and Registration Procedures

[RFC2616]: https://tools.ietf.org/html/rfc2616 "RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1"
\[[RFC2616]\]: RFC 2616 - Hypertext Transfer Protocol -- HTTP/1.1

### A.1 Informative

[TCP]: https://tools.ietf.org/html/rfc793 "RFC 793 - Transmission Control Protocol"
\[[TCP]\]: RFC 793 - Transmission Control Protocol

[Websockets]: https://tools.ietf.org/html/rfc6455 "RFC 6455 - The WebSocket Protocol"
\[[Websockets]\]: RFC 6455 - The WebSocket Protocol
