# 一 、介绍
Linux是个多用户多任务的分时操作系统，所有一个要使用系统资源的用户都必须先向系统管理员申请一个账号，然后以这个账号的身份进入系统。用户的账号一方面能帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也能帮助用户组织文件，并为用户提供安全性保护。每个用户账号都拥有一个惟一的用户名和用户口令。用户在登录时键入正确的用户名和口令后，才能进入系统和自己的主目录。
实现用户账号的管理，要完成的工作主要有如下几个方面：
a.用户账号的添加、删除和修改。
b.用户口令的管理。
c.用户组的管理。

# 二 、用户

## 1.添加用户

useradd 选项 用户名
