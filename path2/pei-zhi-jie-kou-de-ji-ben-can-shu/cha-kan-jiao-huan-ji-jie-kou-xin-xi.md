# 5.8 查看交换机接口信息

在特权模式下，用 show interfaces 命令可查看交换机指定接口的设置和统计信息。

## 模式：

特权模式。

## 命令：

```java
Switch#show interfaces [port-ID] [counters | description | status | switchport | trunk]
```

## 参数：

`port-ID：`可选，指定要查看的接口，可以是物理接口、VLAN或Aggregate Port接口。

`counters：`可选，只查看接口的统计信息。

`description：`可选，只查看接口的描述信息。

`status：`可选，查看接口的各种状态信息，包括速率、双工等。

`switchport：`可选，查看2层接口信息，只对2层口有效。

`trunk：`可选，查看接口的Trunk信息。

## 说明：

如果未指定参数，则显示所有接口信息。

## 配置举例：

查看交换机的`fastethernet0/1`口的信息。

```java
Switch>enable
Switch#show interfaces f0/1
Interface : FastEthernet0/1
Description : to-PC1
AdminStatus : up
OperStatus : down
Medium-type : fiber
Hardware : GBIC
Mtu : 1500
LastChange : 0d:0h:0m:0s
AdminDuplex : Auto
OperDuplex : Unknown
AdminSpeed : Auto
OperSpeed : Unknown
FlowControlAdminStatus : Auto
FlowControlOperStatus : Off
Priority : Auto
```

