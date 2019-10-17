# 5.3 交换机接口配置的一般方法

配置接口时，可以配置单个接口，也可以成组配置多个接口。

## 配置单个接口：

```java
Switch(config)#interface port-ID
Switch(config-if)#配置接口参数
```

`interface`命令用于指定一个接口，之后的命令都是针对此接口的。

## 说明：

interface命令可以在全局配置模式下执行，此时会进入接口配置模式，它也可以在接口配置模式下执行，所以配置完一个接口后，可直接用interface命令指定下一个接口。

## 参数：

port-ID是接口的标识，它可以是一个物理接口，也可以是一个VLAN（此时应该把VLAN理解为一个接口），或者是一个Aggregate Port。

## 配置举例：

配置交换机的IP地址为192.168.1.5，并把接口fastethernet0/1和fastethernet0/2设置为全双工模式。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface vlan 1
Switch(config-if)#ip address 192.168.1.5 255.255.255.0
Switch(config-if)#interface f0/1
Switch(config-if)#duplex full
Switch(config-if)#interface f0/2
Switch(config-if)#duplex full
Switch(config-if)#end
Switch#
```

## 说明：

当交换机没有3层口时，所有接口都属于VLAN1，所以VLAN1的IP地址就是交换机的IP地址。

## 成组配置接口：

如果有多个接口需要配置相同的参数时，可以成组配置这些接口。

```java
Switch(config)#interface range port-range
Switch(config-if)#配置接口参数
```

## 参数：

port-range是接口的范围，它可以指定多个范围段，各范围段之间用逗号隔开。

## 说明：

port-range指定接口范围可以是物理接口范围，也可以是一个VLAN范围。如：f0/1-6、vlan 2-4等。

## 注意：

在interface range中的接口必须是相同类型的接口。

## 配置举例：

配置交换机的接口`fastethernet0/1`~`fastethernet0/12`的速度为100Mbps，并把`fastethernet0/1`~`fastethernet0/3`和`fastethernet0/7`~`fastethernet0/10`分配给VLAN2。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface range f0/1-12
Switch(config-if)#speed 100
Switch(config-if)#interface range f0/1-3,0/7-10
Switch(config-if)#switchport access vlan 2
Switch(config-if)#end
Switch#
```

