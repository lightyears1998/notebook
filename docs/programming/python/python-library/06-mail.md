# 邮件

```py
import email.mime.text
import email.header
import email.utils
import ssl
import smtplib


class Mailer:
    def __init__(self, email_config):
        self.server = email_config['server']
        self.content = email_config['content']
        self.sender = email_config['sender']
        assert self.server['encryption'] == 'SSL'  # 不支持其他加密方法

    def send(self, receiver, message) -> None:
        """
        通过邮件设置发送消息
        :param receiver: 收件人
        :param message: 待发送的消息
        :return: None
        """

        mail = email.mime.text.MIMEText(message)
        mail['From'] = email.utils.formataddr((self.content['from'], self.server['username']))
        mail['To'] = receiver
        mail['Subject'] = email.header.Header(self.content['subject'])

        ssl_context = ssl.create_default_context()
        with smtplib.SMTP_SSL(self.server['host'], self.server['port'], context=ssl_context) as mail_client:
            mail_client.login(self.server['username'], self.server['password'])
            mail_client.sendmail(self.sender, receiver, mail.as_string())
```
