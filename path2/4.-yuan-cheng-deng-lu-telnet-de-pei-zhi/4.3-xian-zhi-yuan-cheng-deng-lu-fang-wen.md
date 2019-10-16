# 4.3 限制远程登录访问

当Telnet Server开启时，我们可以配置允许远程登录的IP地址，这样，可以限制用户只能从指定计算机远程登录交换机。

## 模式：

在全局配置模式中配置。

## 配置命令：

```java
Switch(config)#service telnet host host-ip
```

参数 host-ip 为允许远程登录的用户的IP地址。

## 说明：

你可以多次使用此命令设置多个允许远程登录的合法用户IP。如果不配置此项，默认是不限制使用者的IP地址。

## 删除配置的Telnet限制：

`Switch(config)#no service telnet host host-ip`

此命令只删除指定的IP。

`Switch(config)#no service telnet host`

此命令删除所有的IP。

## 配置举例：

只允许IP地址为192.168.1.10和192.168.1.30的用户用Telnet登录交换机。

```java
Switch>enable
Switch#configure terminal
Switch(config)#service telnet host 192.168.1.10
Switch(config)#service telnet host 192.168.1.30
```

