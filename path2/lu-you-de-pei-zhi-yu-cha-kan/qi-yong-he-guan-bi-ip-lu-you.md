# 9.1 启用和关闭IP路由

要使用交换机的三层功能，必须打开IP路由功能。在S3550系列交换机中，IP路由功能默认是打开的。如果没有打开，需要用命令打开它。

## 1、启用IP路由功能：

```java
Ruijie(config)#ip routing
```

## 说明：

启用IP路由后，连接在三层交换机上的各个子网间就可以互相访问了。你可以使用 show ip route 命令查看路由表。

## 2、关闭IP路由功能：

```java
Ruijie(config)#no ip routing
```

## 配置举例：

交换机的fastethernet0/1连接了一个子网192.168.1.0/24，fastethernet0/2连接了一个子网192.168.2.0/24。利用交换机的3层功能使它们能够通信。

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#interface f0/1
Ruijie(config-if)#no switchport
Ruijie(config-if)#ip address 192.168.1.1 255.255.255.0
Ruijie(config-if)#interface f0/2
Ruijie(config-if)#no switchport
Ruijie(config-if)#ip address 192.168.2.1 255.255.255.0
Ruijie(config-if)#exit
Ruijie(config)#ip routing
Ruijie(config)#exit
Ruijie#show ip route
```

本例中，首先把 f0/1 和 f0/2 都配置为3层路由口，并配置了IP地址。之后用 ip routing 命令启用IP路由。在路由表中应该可以看到网络 192.168.1.0/24 和 192.168.2.0/24 的路由表项。

## 配置静态路由

静态是手工添加的路由项目。

## 模式：

全局配置模式。

## 1、配置静态路由：

```java
Ruijie(config)#ip route network-number network-mask ip-address
```

## 参数：

`network-number`是目的地址，一般是一个网络地址。

`network-mask` 是目的地址的子网掩码。

`ip-address` 是下一跳地址。

## 说明：

ip route命令定义的是一条传输路径，可以告知设备把某个地址的数据报送往何处。配置完成后可以使用 show ip route 命令查看路由表。

## 2、删除静态路由：

```java
Ruijie(config)#no ip route network-number network-mask
```

## 配置举例1：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#ip route 172.16.0.0 255.255.0.0 192.168.3.2
```

`ip route 172.16.0.0 255.255.0.0 192.168.3.2` 命令表示把所有目的地址在`172.16.0.0/16`网络中的数据报发往地址 `192.168.3.2` 处。

## 配置举例2：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#no ip route 172.16.0.0 255.255.0.0
```

本例删除了路由表中目的地址为172.16.0.0/16网络的静态路由。

