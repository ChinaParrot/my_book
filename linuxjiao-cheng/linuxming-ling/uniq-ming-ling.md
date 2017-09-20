uniq命令用于报告或忽略文件中的重复行，一般与sort命令结合使用，类似于sort -u

```
-c或——count：在每列旁边显示该行重复出现的次数；
-u或——unique：仅显示出一次的行列； 
-d或--repeated：仅显示重复出现的行列；

-f<栏位>或--skip-fields=<栏位>：忽略比较指定的栏位； 
-s<字符位置>或--skip-chars=<字符位置>：忽略比较指定的字符； 
-w<字符位置>或--check-chars=<字符位置>：指定要比较的字符。
```

```
[root@bogon /]# uniq -c /etc/passwd
      1 root:x:0:0:root:/root:/bin/bash
      2 bin:x:1:1:bin:/bin:/sbin/nologin
      1 daemon:x:2:2:daemon:/sbin:/sbin/nologin
      1 adm:x:3:4:adm:/var/adm:/sbin/nologin
      1 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
      2 sync:x:5:0:sync:/sbin:/bin/sync
      1 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
      1 halt:x:7:0:halt:/sbin:/sbin/halt
      1 mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
      1 uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
      1 operator:x:11:0:operator:/root:/sbin/nologin
      1 games:x:12:100:games:/usr/games:/sbin/nologin
      2 gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
      1 ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
      1 nobody:x:99:99:Nobody:/:/sbin/nologin
      1 vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
      1 saslauth:x:499:76:Saslauthd user:/var/empty/saslauth:/sbin/nologin
      1 postfix:x:89:89::/var/spool/postfix:/sbin/nologin
      2 sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
      1 ntp:x:38:38::/etc/ntp:/sbin/nologin
      1 openvpn:x:498:498:OpenVPN:/etc/openvpn:/sbin/nologin
      1 nginx:x:497:497::/home/nginx:/sbin/nologin
      1 xjq:x:500:500::/home/xjq:/bin/bash
[root@bogon /]# uniq -d /etc/passwd
bin:x:1:1:bin:/bin:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
[root@bogon /]# uniq -d /etc/passwd
```



