# 4.2 在三层交换机上配置DoS过滤

在缺省情况下，3层交换机的预防DoS攻击的入口过滤功能是关闭的，配置时，需要打开该服务。

## 1、打开预防DoS攻击入口过滤的开关：

## 模式：

接口配置模式。

## 命令：

```java
Switch(config-if)#ip deny spoofing-source
```

这条命令用于打开指定接口的入口过滤开关。

## 说明：

1. 这条命令只能用于3层口。
2. 过滤开关打开后，系统会自动为该接口生成一个ACL，ACL的名称为`auto_defeat_dos_interfaceID`，其中`interfaceID`是接口名。假设这个3层口的IP地址是`192.168.5.1/24，`则生成的ACL的内容为：

```java
permit 192.168.5.0 0.0.0.255
permit host 0.0.0.0
deny any
```

这个ACL会作用在接口的传入检查中，它只允许源地址和192.168.5.0匹配的数据报传入，以及源地址为0.0.0.0的数据报传入（这种数据报是DHCP请求报文），如果源地址是其它值，说明是伪造的，交换机会直接把它丢弃。

1. 你只能在和下层网段直连的接口上配置过滤功能，不要在和上层网络相连的接口（如Uplink口）上配置过滤功能，这会导致源自Internet的各种源IP报文无法进入该网段。
2. 如果在接口上有一个自定义的ACL，则它不能和过滤生成的ACL同时应用。解决方法是不开启过滤功能，但在自定义的ACL中加入过滤用的语句。
3. 在设置了过滤功能后，如果修改了接口的IP地址，必须先关闭过滤功能然后再打开，这样才能使入口过滤对新的地址生效。

## 2、关闭入口过滤功能：

## 模式：

接口配置模式。

## 命令：

```java
Switch(config-if)#no ip deny spoofing-source
```

## 3、查看入口过滤配置：

## 模式：

特权模式。

## 命令：

```java
Switch#show access-group
```

本命令用于查看ACL。

## 配置举例1：

在一个3层路由口上启用入口过滤功能。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/3
Switch(config-if)#no switchport
Switch(config-if)#ip address 192.168.30.1 255.255.255.0
Switch(config-if)#ip deny spoofing-source
Switch(config-if)#end
Switch#
```

配置后会生成一个名为`auto_defeat_dos_fastethernet_3`的ACL，并且被关联在f0/3的传入端，它会禁止源IP为192.168.30.0以外的数据报从此接口进入交换机。（DHCP请求报文除外）

## 配置举例2：

在一个3层SVI接口上启用入口过滤功能。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface vlan 2
Switch(config-if)#ip address 192.168.120.1 255.255.255.0
Switch(config-if)#ip deny spoofing-source
Switch(config-if)#end
Switch#
```

配置后会生成一个名为`auto_defeat_dos_vlan_2`的ACL，并且被关联在vlan 2的传入端，它会禁止源IP为192.168.120.0以外的数据报从此接口进入交换机。（DHCP请求报文除外）

