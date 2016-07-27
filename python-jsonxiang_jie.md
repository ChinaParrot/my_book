# python-json详解


##一、介绍

* JSON全称是Javascript Object Notation，很明显，是源于Javascript。此处暂可不深究这方面，知道这点即可。
* JSON是一种字符串，有一定特定的语法格式的字符串；
* JSON之所以定义这样的语法格式，目的在于方便数据的交换。即，一些数据，通过JSON这种格式，从一个地方，尤其是网络上，发送，传递到另外一个地方，然后使得接受者，也很容易理解相关的数据。

##二、语法

*  对象，即一个变量名，一个值，对应的写法是：{name:value}
*  列表，有多个元素是，写法是：[collection, collection]
*  余下的，按照正常逻辑理解即可，比如字符串是两个双引号""括起来的，数字是0到9等等。

##三、举例

```
{
     "firstName": "John",
     "lastName": "Smith",
     "male": true,
     "age": 25,
     "address": 
     {
         "streetAddress": "21 2nd Street",
         "city": "New York",
         "state": "NY",
         "postalCode": "10021"
     },
     "phoneNumber": 
     [
         {
           "type": "home",
           "number": "212 555-1234"
         },
         {
           "type": "fax",
           "number": "646 555-4567"
         }
     ]
 }
```
通过此例子，也就算很形象的知道了，JSON算是一个结构很清晰的，用于表示数据的一种格式。
