# 4.4 设置远程登录的超时时间

当你用Telnet登录交换机后，如果在设定的超时时间内没有任何输入，交换机会自动断开该连接，所以设置超时时间有一定的保护作用。

Telnet的超时时间默认为5分钟，你可以用命令修改它。

## 模式：

线路配置模式

## 配置命令：

```java
Switch(config-line)#exec-timeout time
```

参数 time 为设置的超时时间，单位为秒，取值为0~3600，如果设置为0，表示不限定超时时间。

## 说明：

你必须先用 line vty 命令进入远程登录的线路模式再配置超时时间。

## 删除配置的Telnet超时时间：

```java
Switch(config-line)#no exec-timeout
```

删除后，超时时间恢复为默认的5分钟。

## 配置举例：

设置远程登录的超时时间为10分钟（600秒）。

```java
Switch>enable
Switch#configure terminal
Switch(config)#line vty
Switch(config-line)#exec-timeout 600
```

