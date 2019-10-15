# 2.2 DHCP代理的配置

在缺省情况下，3层交换机的DHCP代理服务是关闭的，配置时，需要打开该服务。

## 1、打开DHCP Relay Agent：

## 模式：

全局配置模式。

## 命令：

```java
Switch(config)#service dhcp
service dhcp命令用于打开DHCP Relay Agent，这时，交换机就可以进行代理工作了。
```

## 2、配置DHCP Server的IP地址：

如果没有指定DHCP服务器的IP地址，交换机会以255.255.255.255为地址转发DHCP请求，这种转发是向所有接口转发，我们不推荐这种做法。解决方法就是把DHCP服务器的IP地址告知交换机。

## 模式：

全局配置模式。

## 命令：

```java
Switch(config)#ip helper-address IP-address
```

这条命令用于指定DHCP服务器的IP地址。

## 3、关闭DHCP代理：

在全局配置模式下，可以用 `no ip helper-address` 命令把DHCP Server的IP地址恢复为默认值，用 `no service dhcp` 命令可以关闭交换机的DHCP Relay Agent功能。

## 4、查看DHCP Relay Agent状态：

在特权模式下，可以用 show ip management 命令查看DHCP Relay Agent状态。

## 配置举例：

已知DHCP服务器的IP地址为192.168.1.15，把交换机配置成DHCP Relay Agent。

```java
Switch>enable
Switch#configure terminal
Switch(config)#service dhcp
Switch(config)#ip helper-address 192.168.1.15
Switch(config)#end
Switch#
```

## 说明：

想要实现多网段的DHCP服务功能，除了把交换机配置为DHCP Relay Agent外，还需要把DHCP服务器配置成可为多网段提供IP地址的工作方式，相关内容请参考DHCP服务器的配置。

