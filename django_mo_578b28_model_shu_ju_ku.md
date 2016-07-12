# Django 模型(model)数据库


添加记录时它会自动增长。你通常不需要直接使用这个字段；# Django 模型(model)数据库

model是对有关数据信息的单一，可靠的信息源。它包含了你存储的数据的必要字段和行为。一般情况下，每个模型映射到单个数据库表。

以下参数适用于所有字段类型。所有这些都是可选的。
如果为True，Django将在数据库中存储空值NULL，默认是False。

unique=True
blank=True
null=True


1、**CharField：**字符串字段，单行输入，用于较短的字符串，如要保存大量文本, 使用 TextField，
控制字符串大小max_length： models.CharField(max_length=大小)

<pre>
from django.db import models
class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
</pre>

2、**AutoField：** 一个自动递增的整型字段，添加记录时它会自动增长。你通常不需要直接使用这个字段；如果你不指定主键的话，系统会自动添加一个主键字段到你的model。

3、**BooleanField：**布尔字段,管理工具里会自动将其描述为checkbox。

4、**TextField**：一个容量很大的文本字段。

5、**DateField：**日期字段，admin 用一个文本框 ```<input type=”text”>``` 来表示该字段数据(附带一个 JavaScript 日历和一个”Today”快捷按键。有下列额外的可选参数：


> auto_now：当对象被保存时,自动将该字段的值设置为当前时间.通常用于表示 “last-modified” 时间戳；
auto_now_add：当对象首次被创建时,自动将该字段的值设置为当前时间.通常用于表示对象创建时间。



6、**DateTimeField：**类似 DateField 支持同样的附加选项。

7、**TimeField**：时间字段，类似于 DateField 和 DateTimeField。

8、**EmailField：**一个带有检查 Email 合法性的 CharField，不接受 maxlength 参数。

<pre>
    created = models.DateTimeField(auto_now_add=True)
    modified = models.DateTimeField(auto_now=True)
</pre>

9、**FloatField**：浮点型字段。 必须提供两个 参数， 参数描述：


> max_digits：总位数(不包括小数点和符号)
decimal_places：小数位数。如：要保存最大值为 999 (小数点后保存2位)，你要这样定义字段：models.FloatField(…，max_digits=5， decimal_places=2)，要保存最大值一百万(小数点后保存10位)的话，你要这样定义：models.FloatField(…，max_digits=19， decimal_places=10)

10、自定义user model

不要忘了在settings.py中设置:
 
 AUTH_USER_MODEL = "myapp.User" 

<pre>
 
 from django.contrib.auth.models import AbstractUser
 from django.db import models
 
class User(AbstractUser):
    USER_ROLE_CHOICES = (
        ('SU', 'SuperUser'),
        ('GA', 'GroupAdmin'),
        ('CU', 'CommonUser'),
    )
    name = models.CharField(max_length=80)
    uuid = models.CharField(max_length=100)
    role = models.CharField(max_length=2, choices=USER_ROLE_CHOICES, default='CU')
    group = models.ManyToManyField(UserGroup)
    ssh_key_pwd = models.CharField(max_length=200)
    # is_active = models.BooleanField(default=True)
    # last_login = models.DateTimeField(null=True)
    # date_joined = models.DateTimeField(null=True)

    def __unicode__(self):
        return self.username
     </pre>   