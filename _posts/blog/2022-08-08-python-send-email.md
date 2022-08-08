---
layout: post
title: 关于使用python发送邮件提醒
categories: Blog
description: none
keywords: 博客

---

z在运行时间比较长的服务器后台程序(租用)时，往往需要等待很长时间，而程序运行时间是一个不确定的，因此需要发送邮件来进行程序执行完毕的提醒。以下是示例代码。

```python
import smtplib
from email.mime.text import MIMEText
from email.header import Header

def send_emal(mail_msg="这是一封python自动发送的邮件", receivers=['接收方邮箱@qq.com']):
    # 邮件内容
    mail_msg = mail_msg
    message = MIMEText(mail_msg, 'html', 'utf-8')
    # 发件人名字
    message['From'] = Header('XXX', 'utf-8')
    # 收件人名字
    message['To'] = Header('你好xxx', 'utf-8')
    # 邮件标题
    subject = 'python邮件代码提醒'
    message['subject'] = Header(subject, 'utf-8')
    # 发送方
    sender = '发送方邮箱@qq.com'
    # 接收方
    receivers = receivers
    # 使用QQ邮箱的服务，发送邮件
    smtpObj = smtplib.SMTP_SSL("smtp.qq.com", 465)
    smtpObj.login(sender, '这里输入授权码')
    smtpObj.sendmail(sender, receivers, message.as_string())
    smtpObj.quit()
    print('邮件发送成功')
```

需要注意的是，需要获取发送方邮箱的授权码，在邮箱登陆后的设置界面，找到SMTP，获得授权即可。

参考链接：https://www.zhihu.com/zvideo/1252029036924080128