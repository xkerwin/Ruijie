# 4.2 开启和禁止远程登录

默认情况下，Telnet Server是打开的，任何人都可以用Telnet访问交换机，我们可以用命令禁止使用Telnet访问交换机。

## 模式：

在全局配置模式中配置。

## 关闭Telnet Server：

```java
Switch(config)#no enable service telnet-server
```

## 开启Telnet Server：

```java
Switch(config)#enable service telnet-server
```

## 说明：

关闭Telnet访问不影响使用控制台、Web和SNMP访问交换机。

## 配置举例：

关闭交换机的远程登录访问。

```java
Switch>enable
Switch#configure terminal
Switch(config)#no enable service telnet-server
```

