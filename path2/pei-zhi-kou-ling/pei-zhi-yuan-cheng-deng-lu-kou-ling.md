# 2.2 配置远程登录口令

远程登录口令是通过Telnet登录交换机或路由器时设置的口令。

## 1、设置远程登录口令

## 模式：

线路配置模式。

## 配置命令：

```java
Ruijie(config)#line vty 0 4
Ruijie(config-line)#password password
Ruijie(config-line)#login
```

`line vty 0 4` 命令表示配置远程登录线路，0~4是远程登录的线路编号。

`login` 命令用于打开登录认证功能。

`password password` 为远程登录线路设置口令。

## 说明：

设置的口令长度最大长度为25个字符。口令中不能有问号和其他不可显示的字符。如果口令中有空格，则空格不能位于最前面，只有中间和末尾的空格可作为口令的一部分。

在 `running-config` 中可以查看口令设置，但锐捷设备的口令都是以密文存放的，所以看到的是乱码。

## 注意：

远程登录口令是用Telnet登录的必备条件。

## 2、删除配置的远程登录口令：

```java
Ruijie(config)#line vty 0 4
Ruijie(config-line)#no password
```

配置举例：为交换机设置远程登录密码为123。

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#line vty 0 4
Ruijie(config-line)#login
Ruijie(config-line)#password 123
Ruijie(config-line)#end
Ruijie#
```

本例设置远程登录口令为123。

