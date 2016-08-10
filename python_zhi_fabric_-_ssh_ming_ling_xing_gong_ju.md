# python 之Fabric-SSH命令行工具


Fabric是基于python2.5及以上版本实现的SSH命令行工具，简化了SSH应用程序部署及系统管理任务，他提供了系统基础的操作组件，可以实现本地或远程shell命令，包括命令执行、文件上传、下载及完整执行日志输出等功能。Fabric在paramiko的基础上做更高一层的封装，操作起来更加简单。

官网地址：http://www.fabfile.org/

##fab的常用参数
Usage: fab [options] <command>[:arg1,arg2=val2,host=foo,hosts='h1;h2',...] ...
