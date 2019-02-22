# uWSGI Python网关

- Web Server Gateway Interface
- uwsgi协议

## 配置

与Nginx配合使用

```conf
server {
    listen 3030;                     # Nginx监听3030端口与用户端应用程序通信
    client_max_body_size 10m;        # POST消息体最大长度 10MB

    location / {
        include uwsgi_params;        # 传递必要的参数
        uwsgi_pass 127.0.0.1:2929;   # UWSGI监听端口
    }
}
```

ini配置文件 `uwsgi --ini "config.ini"`

```ini
[uwsgi]
uid = nginx
socket = 127.0.0.1:2929
processes = 2
threads = 2
wsgi-file = gateway/gateway.py
thunder-lock = 1
py-autoreload = 1
post-buffering = 1
```
