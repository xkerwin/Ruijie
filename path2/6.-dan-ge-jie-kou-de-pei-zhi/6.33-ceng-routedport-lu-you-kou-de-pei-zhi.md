# 6.3 3层Routed Port（路由口）的配置

3层交换机的所有接口默认都是2层Access Port，需要经过配置，才能使某个接口成为3层路由口。

Routed接口具有以下特性：

1. Routed接口是3层口，我们可以为它配置一个IP地址。
2. 每个Routed接口可用于连接一个子网，Routed接口的IP地址就是该子网的网关。
3. 如果一台交换机配置了多个3层口，各个3层口的IP地址应属于不同的网络。

## 1、把一个Access接口配置为Routed接口：

```java
Switch(config)#interface port-id
Switch(config-if)#no switchport
Switch(config-if)#ip address IP-address Subnet-Mask
```

`interface` 命令用于指定要修改的接口，这个接口只能是物理接口。 `no switchport` 命令用于把2层`Access Port`设置为3层`Routed Port`。 `ip address` 命令用于给3层`Routed Port`设置IP地址和子网掩码。

## 说明：

每个3层路由口只能对应一个物理接口。只有3层口才能配置IP地址，2层口不能配置IP地址。

## 2、把一个Routed接口还原为Access接口：

```java
Switch(config)#interface port-id
Switch(config-if)#switchport
```

## 配置举例：

把FastEthernet0/1配置为3层Routed Port，并设置IP地址。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#no switchport
Switch(config-if)#ip address 192.168.2.1 255.255.255.0
Switch(config-if)#end
Switch#
```

