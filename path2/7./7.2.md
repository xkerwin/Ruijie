# 7.2 SVI的配置

如果给一个VLAN配置上IP地址，它就成为一个SVI接口，它具有以下特性：

SVI接口由多个物理接口组成，但在逻辑上，可把它理解为一个3层口。 每个SVI接口可用于连接一个子网，SVI接口的IP地址就是该子网的网关。 组成SVI的物理接口都必须是Access接口，不能是3层口。

## 1、配置SVI接口：

```java
Switch(config)#interface vlan vlan-id
Switch(config-if)#ip address IP-address Subnet-Mask
```

`interface` 命令用于指定一个VLAN。

`ip address` 命令用于给这个VLAN设置IP地址和子网掩码，使它成为SVI接口。

## 2、恢复SVI为VLAN：

```java
Switch(config)#interface vlan vlan-id
Switch(config-if)#no ip address
```

## 配置举例：

配置一个SVI，其中包含了FastEthernet0/1和FastEthernet0/2两个接口。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#switchport access vlan 20
Switch(config-if)#interface f0/2
Switch(config-if)#switchport access vlan 20
Switch(config-if)#interface vlan 20
Switch(config-if)#ip address 192.168.10.1 255.255.255.0
Switch(config-if)#end
Switch#
```

