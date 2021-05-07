# nginx reverse proxy

This project shows how to access multiple ports over public URL using nginx reverse proxy. 
Note: this is not production ready.
MODIFY /NGINX/HTTP.CONF WITH HASS CONFIGURATOTOR FILE NAME IN DOCKER IS /etc/nginx/conf.d/default.conf


 THROUGH PROXY HASS CONGIF WORKING BUT HOME ASSISTANT LOGIN PROBLEM
 
 
 may be solution not tried
 Rewriting Requests
Now as you might have noticed in Step 6, nginx sends the same
HTTP request to your `node.js` web apps which results into a 404 error.
Why? Because, your `node.js` web application serves requests from `/`
not from `/blog` and `/mail`. But, `nginx` is sending requests to `/blog` and
`/mail`.

To fix this issue, we need rewrite the URL so that it matches the URL
you can serve on your `node.js` applications.

To correctly rewrite URLs change your config file to match the following snippet:

```
server {
    listen       ...;
    ...
    location / {
        proxy_pass http://127.0.0.1:8080;
    }
    
    location /blog {
        rewrite ^/blog(.*) /$1 break;
        proxy_pass http://127.0.0.1:8181;
    }

    location /mail {
        rewrite ^/mail(.*) /$1 break;
        proxy_pass http://127.0.0.1:8282;
    }
    ...
}
```


more help in nginx.md
