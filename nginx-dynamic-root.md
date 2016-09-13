# Nginx Dynamic Root Config

### Implement the following url
```
http://yii2-test-frontend.app  
http://yii2-test-frontend.app/backend/
```

```nginx
server {
    listen 80;
    listen 443 ssl;
    server_name yii2-test-frontend.app;
    set $root "/home/vagrant/workspace/local/yii2-test/frontend/web";
    set $orgscript "";

    if ($request_uri ~* ^/phpmyadmin/) {
        set $root "/home/vagrant/workspace/local/yii2-test/phpmyadmin";
        rewrite ^/phpmyadmin/(.*) /$1 last;
    }

    if ($request_uri ~* ^/backend/) {
        set $root "/home/vagrant/workspace/local/yii2-test/backend/web";
        set $orgscript "/backend";
        rewrite ^/backend/(.*) /$1 last;
    }

    root $root;
    error_log /home/vagrant/nginx-error.log debug_http;
    index index.html index.htm index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    access_log off;
    error_log  /var/log/nginx/yii2-test-frontend.app-error.log error;

    sendfile off;

    client_max_body_size 100m;

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param SCRIPT_NAME $orgscript$fastcgi_script_name;

        fastcgi_intercept_errors off;
        fastcgi_buffer_size 16k;
        fastcgi_buffers 4 16k;
        fastcgi_connect_timeout 300;
        fastcgi_send_timeout 300;
        fastcgi_read_timeout 300;
    }

    location ~ /\.ht {
        deny all;
    }

    ssl_certificate     /etc/nginx/ssl/yii2-test-frontend.app.crt;
    ssl_certificate_key /etc/nginx/ssl/yii2-test-frontend.app.key;
}
```
