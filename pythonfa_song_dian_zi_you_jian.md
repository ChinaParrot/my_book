# Python发送电子邮件

1. MUA: Mail User Agent——邮件用户代理。

2. MTA：Mail Transfer Agent——邮件传输代理，就是那些Email服务提供商，比如网易、新浪等等。

3. MDA：Mail Delivery Agent——邮件投递代理。

# 一、SMTP发送邮件

SMTP是发送邮件的协议，Python内置对SMTP的支持，可以发送纯文本邮件、HTML邮件以及带附件的邮件。



Python对SMTP支持有smtplib和email两个模块，email负责构造邮件，smtplib负责发送邮件。



SMTP类具有如下方法：



