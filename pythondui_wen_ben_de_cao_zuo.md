# python对文件操作

**文件的读取**

```
>>> f=file('contact_list.txt','a')
>>> f.write('\n26\tLizhili\tIt\t2222222222')
>>> f.close
```

```
#/usr/bin/python
import sys
contact_list='contact_list.txt'
f=file(contact_list)
c=f.readlines()

while True:
user_input = raw_input('\033[0;31;1m please input sth to search: \033[0m')
if len(user_input) == 0:
continue
for line in c:
if user_input in line:
print line
elif user_input == "a" or user_input == "quit":
sys.exit()

else:
print "\033[1;32m not in world key word! \033[0m"
```

**文件修改和替换**



