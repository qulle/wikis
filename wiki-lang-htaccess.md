# Living document of useful .htaccess config

## Enable rewrite engine and directory listing
```apacheconf
RewriteEngine on
Options +MultiViews
Options +Indexes
```

## Page to load when visiting the root
```apacheconf
DirectoryIndex service.php index.php
```

## ErrorDocuments    
```apacheconf
ErrorDocument 403 /forbidden.php
ErrorDocument 401 /forbidden.php
ErrorDocument 404 /lost.php
ErrorDocument 500 /error.php
```

## Allow no extension and redirec to the non-extension page
```apacheconf
RewriteCond %{THE_REQUEST} /([^.]+)\.php [NC]
RewriteRule ^ /%1 [NC,L,R]

RewriteCond %{REQUEST_FILENAME}.php -f
RewriteRule ^(.*)$ $1.php  [NC,L]
```

## Redirect all traffic to https
```apacheconf
RewriteCond %{HTTPS} !=on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

## Prevent image hotlinking
```apacheconf
RewriteCond %{HTTP_REFERER} !^$
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?my-domain.com [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?utv.my-domain.local [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?google.com [NC]
RewriteCond %{HTTP_REFERER} !^http(s)?://(www\.)?facebook.com [NC]
RewriteRule \.(jpg|jpeg|png|gif|svg)$ - [F]
```

## Disable Varnish cache      
```apacheconf
Header add "Cache-Control" "no-cache"
```

## Permanent redirect
```apacheconf
Redirect 301 /oldpage.php https://www.my-domain.com/new-page.php
```
