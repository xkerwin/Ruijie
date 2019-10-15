# 11.1 OSPF协议的一般配置

## 1、配置OSPF协议：

```java
Ruijie(config)#router ospf process-id
Ruijie(config-router)#network network-number wildcard-mask area area-id
```

`router ospf` 命令用于启用OSPF，并进入OSPF的配置模式。`process-id`是进程号，用于路由器内部。

`network` 命令用于指定参与OSPF路由的网络，参数`network-number`是网络号，`wildcard-mask`是通配符掩码，`area-id`是区域号。

## 说明：

通配符掩码用于指定网络号中有效的位，取“0”代表匹配该位，取“1”代表忽略该位。很多情况下，通配符掩码是子网掩码的反码。

路由配置好后，可以在特权模式下用 `show ip route` 命令查看学习到的路由项目。

## 2、删除OSPF中配置的项目：

```java
Ruijie(config)#router ospf
Ruijie(config-router)#no network network-number wildcard-mask area area-id
```

## 3、关闭OSPF协议：

```java
Ruijie(config)#no router ospf process-id
```

关闭后，本设备的OSPF协议将不再工作。

## 配置举例1：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#router ospf 1
Ruijie(config-router)#network 192.168.1.0 0.0.0.255 area 0
Ruijie(config-router)#network 192.168.5.0 0.0.0.255 area 0
Ruijie(config-router)#end
```

本例在设备上启用了OSPF协议，关联的网络是 192.168.1.0/24 和 192.168.5.0/24。

## 配置举例2：

```java
Switch>enable
Switch#configure terminal
Switch(config)#router ospf 1
Switch(config-router)#network 192.168.0.0 0.0.255.255 area 0
Switch(config-router)#end
```

本例在设备上启用了OSPF协议，关联的网络是所有形如 192.168.0.0 的网络。

