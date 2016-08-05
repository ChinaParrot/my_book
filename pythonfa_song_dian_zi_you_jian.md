 #Python发送电子邮件

1. MUA: Mail User Agent——邮件用户代理。
2. MTA：Mail Transfer Agent——邮件传输代理，就是那些Email服务提供商，比如网易、新浪等等。
3. MDA：Mail Delivery Agent——邮件投递代理。

##一、SMTP发送邮件


SMTP是发送邮件的协议，Python内置对SMTP的支持，可以发送纯文本邮件、HTML邮件以及带附件的邮件。

Python对SMTP支持有smtplib和email两个模块，email负责构造邮件，smtplib负责发送邮件。

SMTP类具有如下方法：


* SMTP.connect([host[, port]])方法，连接远程smtp主机方法，host为远程主机地址，port为远程主机smtp端口，默认25，也可以直接使用host:port形式来表示，例如：SMTP.connect（“smtp.163.com”，“25”）。
* SMTP.login(user, password)方法，远程smtp主机的校验方法，参数为用户名与密码，如SMTP.login（“python_2014@163.com”，“sdjkg358”）。
* SMTP.sendmail(from_addr, to_addrs, msg[, mail_options, rcpt_options])方法，实现邮件的发送功能，参数依次为是发件人、收件人、邮件内容，例如：SMTP.sendmail（“python_2014@163.com”，“demo@domail.com”，body），其中body内容定义如下： 

```
"""From: python_2014@163.com
To: demo@domail.com
Subject: test mail
test mail body"""
``` 
* SMTP.starttls([keyfile[, certfile]])方法，启用TLS（安全传输）模式，所有SMTP指令都将加密传输，例如使用gmail的smtp服务时需要启动此项才能正常发送邮件，如SMTP.starttls()。

* SMTP.quit()方法，断开smtp服务器的连接。

###1. 如果我们本机没有 sendmail等，也可以使用其他邮件服务商的 SMTP（QQ、网易、Google等）。

<pre>
#!/usr/bin/python
#-*- coding:UTF-8 -*-

import smtplib
from email import encoders
from email.header import Header
from email.mime.text import MIMEText
from email.utils import parseaddr, formataddr

def _format_addr(s):
      name, addr = parseaddr(s)
      return formataddr((Header(name, 'utf-8').encode(), addr))

from_addr = '1362832155@qq.com'
password = '123456'
smtp_server = 'smtp.qq.com'
to_addr = '532748570@saidian.com'

msg = MIMEText('hello, my first mail...','plain','utf-8')
msg['From'] = _format_addr('Python爱好者 <%s>' %from_addr)
msg['To'] = _format_addr('jqlinux <%s>' %to_addr)
msg['Subject'] = Header('test','utf-8').encode()

server = smtplib.SMTP_SSL(smtp_server, 465)
#server = smtplib.SMTP(smtp_server, 25)
server.set_debuglevel(1)
server.login(from_addr, password)
while 1:
  try:
	server.sendmail(from_addr, [to_addr], msg.as_string())
	break
  except:
	  try:
	      smtp.connect(smtp_server)#连接至邮件服务器
	      smtp.login(from_addr, password)#登录邮件服务器
	  except:
	      print "failed to login to smtp server"#登录失败
server.quit()

</pre>

###2. 使用Python发送HTML格式的邮件

<pre>
#!/usr/bin/python
#-*- coding:UTF-8 -*-

import smtplib
from email import encoders
from email.header import Header
from email.mime.text import MIMEText
from email.utils import parseaddr, formataddr

def _format_addr(s):
      name, addr = parseaddr(s)
      return formataddr((Header(name, 'utf-8').encode(), addr))

from_addr = '1362832155@qq.com'
password = '123456'
smtp_server = 'smtp.qq.com'
to_addr = '532748570@saidian.com'

mail_msg = """
<p>Python 邮件发送测试...</p>
<p><a href="https://jqlinux.com">这是一个链接</a></p>
"""
msg = MIMEText(mail_msg,'html','utf-8')
msg['From'] = _format_addr('Python爱好者 <%s>' %from_addr)
msg['To'] = _format_addr('jqlinux<%s>' %to_addr)
msg['Subject'] = Header('test','utf-8').encode()

server = smtplib.SMTP_SSL(smtp_server, 465)
#server = smtplib.SMTP(smtp_server, 25)
server.set_debuglevel(1)
server.login(from_addr, password)
while 1:
  try:
	server.sendmail(from_addr, [to_addr], msg.as_string())
	break
  except:
	  try:
	      smtp.connect(smtp_server)#连接至邮件服务器
	      smtp.login(from_addr, password)#登录邮件服务器
	  except:
	      print "failed to login to smtp server"#登录失败
server.quit()
</pre>

##3. Python 发送带附件的邮件

<pre>
#!/usr/bin/python
#-*- coding:UTF-8 -*-

import smtplib
from email import encoders
from email.header import Header
from email.mime.text import MIMEText
from email.utils import parseaddr, formataddr
from email.mime.multipart import MIMEMultipart

def _format_addr(s):
      name, addr = parseaddr(s)
      return formataddr((Header(name, 'utf-8').encode(), addr))

from_addr = '1362832155@qq.com'
password = 'xjq1206$'
smtp_server = 'smtp.qq.com'
to_addr = 'xuejq@saidian.com'


#带附件的实例
message = MIMEMultipart()
message['From'] = _format_addr('Python爱好者 <%s>' %from_addr)
message['To'] = _format_addr('jqlinux <%s>' %to_addr)
message['Subject'] = Header('test','utf-8').encode()

#邮件正文内容
message.attach(MIMEText('+++++++++++++++++++++test++++++++++++++++++++++++++++','plain','utf-8'))


# 构造附件1，传送当前目录下的 dump.txt 文件
att1 = MIMEText(open('dump.txt', 'rb').read(), 'base64', 'utf-8')
att1["Content-Type"] = 'application/octet-stream'
# 这里的filename可以任意写，写什么名字，邮件中显示什么名字
att1["Content-Disposition"] = 'attachment; filename="dump.txt"'
message.attach(att1)

# 构造附件2，传送当前目录下的 mail.py 文件
att2 = MIMEText(open('mail.py', 'rb').read(), 'base64', 'utf-8')
att2["Content-Type"] = 'application/octet-stream'
att2["Content-Disposition"] = 'attachment; filename="mail.py"'
message.attach(att2)


server = smtplib.SMTP_SSL(smtp_server, 465)
#server = smtplib.SMTP(smtp_server, 25)
server.set_debuglevel(1)
server.login(from_addr, password)
while 1:
  try:
	server.sendmail(from_addr,to_addr,message.as_string())
	break
  except:
	  try:
	      smtp.connect(smtp_server)#连接至邮件服务器
	      smtp.login(from_addr, password)#登录邮件服务器
	  except:
	      print "failed to login to smtp server"#登录失败
server.quit()

</pre>

###4. 在 HTML 文本中添加图片

<pre>
#!/usr/bin/python
#-*- coding:UTF-8 -*-

import smtplib
from email.mime.image import MIMEImage
from email import encoders
from email.header import Header
from email.mime.text import MIMEText
from email.utils import parseaddr, formataddr
from email.mime.multipart import MIMEMultipart

def _format_addr(s):
      name, addr = parseaddr(s)
      return formataddr((Header(name, 'utf-8').encode(), addr))

from_addr = '1362832155@qq.com'
password = 'xjq1206$'
smtp_server = 'smtp.qq.com'
to_addr = 'xuejq@saidian.com'


#带附件的实例
message = MIMEMultipart()
message['From'] = _format_addr('Python爱好者 <%s>' %from_addr)
message['To'] = _format_addr('jqlinux <%s>' %to_addr)
message['Subject'] = Header('test','utf-8').encode()

#邮件正文内容
message.attach(MIMEText('+++++++++++++++++++++test++++++++++++++++++++++++++++','plain','utf-8'))


mail_msg = """
<p>Python 邮件发送测试...</p>
<p><a href="http://jqlinux.com">jqlinux链接</a></p>
<p>图片演示：</p>
<p><img src="cid:image1"></p>
"""
message.attach(MIMEText(mail_msg, 'html', 'utf-8'))

# 指定图片为当前目录
fp = open('git_config.png', 'rb')
msgImage = MIMEImage(fp.read())
fp.close()

# 定义图片 ID，在 HTML 文本中引用
msgImage.add_header('Content-ID', '<image1>')
message.attach(msgImage)

server = smtplib.SMTP_SSL(smtp_server, 465)
#server = smtplib.SMTP(smtp_server, 25)
server.set_debuglevel(1)
server.login(from_addr, password)
while 1:
  try:
	server.sendmail(from_addr,to_addr,message.as_string())
	break
  except:
	  try:
	      smtp.connect(smtp_server)#连接至邮件服务器
	      smtp.login(from_addr, password)#登录邮件服务器
	  except:
	      print "failed to login to smtp server"#登录失败
server.quit()

</pre>


