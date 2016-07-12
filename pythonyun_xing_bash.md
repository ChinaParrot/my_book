# Python运行bash

python 简单实现运行linux命令：

<pre>
#!/usr/bin/python
#-*- coding: utf-8 -*-

import time
import os
import sys
import shlex
import getpass
current_user=getpass.getuser()#获取当前用户
if current_user != "root":
 print "Error: You must be root to run this script"
 exit()

def bash(cmd):
  """
  执行bash命令
  """
  return shlex.os.system(cmd)
bash('top')
</pre>