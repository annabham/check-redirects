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
Don't do what whatever github is doing for redirects, if you're forwarding to non-www and https.

This is bad practice to have multiple redirects, you can see here:

```
anna@xps:~/scripts$ curl -Is http://www.github.com
HTTP/1.1 301 Moved Permanently
Location: https://www.github.com/

anna@xps:~/scripts$ curl -Is https://www.github.com/
HTTP/1.1 301 Moved Permanently
Location: https://github.com/
```

Do it like this at the top of your .htaccess to be neat, clean, and tidy with your redirects.

```
RewriteCond %{HTTP_HOST} ^www\.github\.com$
RewriteRule ^/?$ "https\:\/\/github\.com\/" [R=301,L]

<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
```
If you want to be tidy with redirecting to www and https, then here's an example on how to do that as well.

```
RewriteCond %{HTTP_HOST} ^github\.com$
RewriteRule ^/?$ "https\:\/\/www\.github\.com\/" [R=301,L]
```
