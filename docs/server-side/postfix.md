# 使用 Postfix 的邮件服务

Postfix 的配置非常灵活，很好用。

``` sh
# 发送邮件
mail -s "Test subject" recipient@domain.com
```

## 所有用户共享一个外部 SMTP 的情景

在 `/etc/postfix/sasl_passwd` 中配置用户名和密码：

``` conf
[smtp.qiye.aliyun.com]:465  account@external.host:password
```

执行后续步骤。

``` sh
chmod 600 /etc/postfix/sasl_passwd
postmap /etc/postfix/sasl_passwd
```

编辑 `/etc/postfix/main.cf`，一种典型的配置如下：

``` conf
relayhost = [smtp.gmail.com]:465
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_security_options =
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
```

在共享一个邮件账户的情况下，需要修改 `From` 字段，[方法](https://serverfault.com/questions/147921/forcing-the-from-address-when-postfix-relays-over-smtp)如下。

``` conf
# /etc/postfix/main.cf

sender_canonical_classes = envelope_sender, header_sender
sender_canonical_maps =  regexp:/etc/postfix/sender_canonical_maps
smtp_header_checks = regexp:/etc/postfix/header_check
```

``` conf
# /etc/postfix/sender_canonical_maps

/.+/   account@external.host
```

``` conf
# /etc/postfix/header_check

/From:.*/ REPLACE From: account@external.host
```
