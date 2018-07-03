# check-redirects
Embarrassingly simple script to check redirects from www to non-www and ssl to non-ssl and vice versa

Usage:  run the script and then enter in the domain or subdomain when prompted

Example:

```
anna@xps:~/scripts$ ./check-redirects.sh 
What is the base domain to check redirects for? github.com
 
==============================
 
Non-www and non-SSL : http://github.com
HTTP/1.1 301 Moved Permanently
Location: https://github.com/
 
==============================
 
www and non-SSL : http://www.github.com
HTTP/1.1 301 Moved Permanently
Location: https://www.github.com/
 
==============================
 
Non-www and SSL : https://github.com
HTTP/1.1 200 OK
 
==============================
 
www and SSL : https://www.github.com
HTTP/1.1 301 Moved Permanently
Location: https://github.com/
 
==============================
```
