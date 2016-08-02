# Python之DNS处理模块dnspython

dnspython（http://www.dnspython.org/）是Python实现的一个DNS工具包，它支持几乎所有的记录类型，可以用于查询、传输并动态更新ZONE信息，同时支持TSIG（事务签名）验证消息和EDNS0（扩展DNS）。在系统管理方面，我们可以利用其查询功能来实现DNS服务监控以及解析结果的校验，可以代替nslookup及dig等工具，轻松做到与现有平台的整合。

