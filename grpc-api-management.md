---
layout: page
title: gRPC API Management
---
[gRPC](https://en.wikipedia.org/wiki/GRPC) is an open source API framework that was created at Google and released in 2016.
It places constraints on API design that make it easier to produce and use high-performing APIs at scale.

**API Description.**
gRPC APIs are usually described with the Protocol Buffers language, and request and response messages use the Protocol Buffer binary encoding. API designs are often expected to conform to style guides like Google's [API Improvement Proposals](https://google.aip.dev/), which increases their consistency and ability to be supported by tools and automation.

**API Implementation.**
gRPC clients and servers are more complex than other API implementations, so they are almost always built on generated code that is produced by tools that are usually open source. gRPC clients and server implementations are also complicated by using advanced networking technologies, including HTTP/2, streaming, and configurable automatic retry. To simplify API consumption, gRPC supports "transcoding", which provides a simpler HTTP/JSON interface to gRPC APIs that have appropriate annotations and follow style guidelines.

gRPC adds additional expectations and opportunities for API management:
* gRPC APIs use Protocol Buffer encoding, so they are more observable, and API management systems can look inside messages to validate or monitor requests and responses.
* Protocol Buffer encoding isn't self-describing, so API management systems can make it easier to use gRPC APIs by providing standard metadata services.
* gRPC APIs are well-defined, so API management systems can easily provide generated documentation and even API client code.
* HTTP/JSON transcoding is also well-defined, so API management systems can provide transcoded versions of gRPC APIs that they manage.
