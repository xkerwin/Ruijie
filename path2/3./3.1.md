# 3.1 配置交换机的管理IP

3层交换机在每个3层口上都可以设置IP地址，这里所说的管理IP是指为一台新交换机设置一个IP地址，使它可以正常访问并管理，将来再根据实际应用配置各3层口的IP地址。

新出厂的交换机在用控制台登录时，可以进行一些基础配置，其中就包括管理IP，你应该在此处配置IP地址等参数。

如果需要修改管理IP，可以在登录后用命令行进行修改。

## 修改管理IP：

```java
Ruijie(config)#interface vlan 1
Ruijie(config-if)#ip address IP-address Subnet-mask
Ruijie(config-if)#no shutdown
```

`interface` 命令用于把管理IP指定给VLAN 1。

`ip address` 命令用于设置IP地址和子网掩码。

## 说明：

通常我们把管理IP指定给VLAN1，因为在初始时，所有接口都属于VLAN1，这样你就可以通过任意一个接口管理交换机了。

## 删除管理IP：

```java
Ruijie(config)#interface vlan 1
Ruijie(config-if)#no ip address
```

## 配置举例：

配置交换机的管理IP为192.168.1.5/24。

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#interface vlan 1
Ruijie(config-if)#ip address 192.168.1.5 255.255.255.0
Ruijie(config-if)#end
Ruijie#
```

## 说明：

在命令中，子网掩码必须采用完整写法，不能简写为/24。

