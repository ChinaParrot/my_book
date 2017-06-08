在远程服务器端生成公私钥：

ssh-keygen -t rsa -b 2048 -P '' -f ~/.ssh/id\_rsa

cat ~/.ssh/id\_rsa.pub &gt;~/.ssh/authorized\_keys 



sshd修改配置文件禁止：

PasswordAuthentication no

PermitRootLogin no





chwon root.root /bin/su

chmod 700 /bin/su





User\_Alias ADMINS = oxuejq

ADMINS  ALL=\(ALL\)       ALL



TMOUT=600



