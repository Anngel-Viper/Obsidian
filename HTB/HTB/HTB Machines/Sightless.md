Level: Easy

Steps :

1. Do an Nmap scan
`nmap 10.10.11.32

2. Try a UDP scan now
`nmap -sU 10.10.11.32 --top-ports=10`

Noting found till now especial

```Not shown: 997 closed tcp ports (conn-refused)  
PORT   STATE SERVICE  
21/tcp open  ftp  
22/tcp open  ssh  
80/tcp open  http
```
The above contains the ports

Lets try a service version scan on this. Also we found an ftp port so lets try bypassing that.

So after looking at the website for a little while longer I found a subdomain of 
http://sqlpad.sightless.htb

Then I added it to the hosts of the pc

After that I looked around at the sqlpad and found two addresses.

1. admin@sightless.htb
2. john@sightless.htb

Then I looked at the site and found that the verison is given. So I search for an exploit and came across one for this. 

https://github.com/0xDTC/SQLPad-6.10.0-Exploit-CVE-2022-0944/blob/master/README.md

Then I made some tweaking in it and finally got it to work and somehow got the admin terminal. Then after that there is a sqlite file in this and tried to cat it out. 

Then after that I found the hashed password of the admin. So right now trying to figure it out.

Admin = 
`$2a$10$cjbITibC.4BQQKJ8NOBUv.p0bG2n8t.RIIKRysR6pZnxquAWsLFcC`
Cracked = admin

Admin2 = Cracked = blindside
`$6$jn8fwk6LVJ9IYw30$qwtrfWTITUro8fEJbReUc7nXyx2wwJsnYdZYm9nMQDHP8SYm33uisO9gZ20LGaepC3ch6Bb2z/lEpBM90Ra4b.`

Found another user Michael
Password = insaneclownposse

Now comes the part of doing privilege escala