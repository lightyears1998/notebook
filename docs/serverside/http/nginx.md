# Nginx笔记

## `nginx.conf`

使用PHP-CGI

```conf
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
location ~ \.php$ {
    root           D:/BitBucket/img.qfstudio.net;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```

```conf
server {
    listen       80;
    server_name  ttrss.qfstudio.net;

    root /home/tt-rss;
    access_log  /var/log/nginx/ttrss.access.log  main;

    location / {
        index  index.html index.htm index.php;
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

## 反向代理

```conf
server {
    server_name host.name;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://localhost:3000;
    }
}
```

## 压缩

```conf
# Compression
gzip            on;
gzip_proxied    expired no-cache no-store private auth;
gzip_types      text/plain text/css application/xml application/javascript;
```

## 缓存

设置了哈希文件名时，可以设置`expire max;`。

```conf
# Cache
## Cache for Image
location ~ \.(gif|jpg|jpeg|png|bmp|ico)$ {
    expires 30d;
}

## Cache for styles and fonts
location ~ \.(css|woff2)$ {
    expires 30d;
}

## Cache for scripts
location ~ \.(js)$ {
    expires 30d;
}
```

---

## Windows

- 访问官网获取预编译的可执行文件。
- 可以使用`winsw`或者`nssm`将`nginx.exe`包装成服务。
- 需要注意在高级安全Windows防火墙中允许`nginx.exe`的通信。

Windows上的路径使用正斜杠为宜。

```conf
location / {
    root   D:/BitBucket/img.qfstudio.net;
    index  index.html index.htm index.php;
}
```
