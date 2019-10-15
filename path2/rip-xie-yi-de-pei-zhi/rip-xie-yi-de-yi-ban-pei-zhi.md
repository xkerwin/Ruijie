# 10.1 RIP协议的一般配置

## 1、配置RIP协议：

```java
Ruijie(config)#router rip
Ruijie(config-router)#network network-number
```

`router rip` 命令用于启用RIP，并进入RIP的配置模式。

`network` 命令用于指定参与RIP路由的网络，它的参数是网络号。如果设备连接了多个网络，你可以用多条 network 命令指定它们；如果要指定设备连接的所有网络，可以用 network 0.0.0.0 来表示所有网络。

## 说明：

对于运行RIP协议的设备，只有用 network 命令指定的网络会参与到RIP发布的路由更新中，可以被其它运行RIP协议的设备学习到；而那些没有用 network 命令指定的网络，不会参与RIP路由，其它设备也不能学习到。

路由配置好后，可以在特权模式下用 `show ip route` 命令查看学习到的路由项目。

## 2、删除RIP关联的网络：

```java
Ruijie(config)#router rip
Ruijie(config-router)#no network network-number
```

## 3、关闭RIP协议：

```java
Ruijie(config)#no router rip
```

关闭后，本设备的RIP协议将不再工作。

## 配置举例1：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#router rip
Ruijie(config-router)#network 192.168.1.0
Ruijie(config-router)#network 192.168.5.0
Ruijie(config-router)#end
```

本例在设备上启用了RIP协议，关联的网络是 192.168.1.0/24 和 192.168.5.0/24。

## 注意：

`192.168.1.0/24` 和 `192.168.5.0/24` 都只能是和本设备直连的网络。

## 配置举例2：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#router rip
Ruijie(config-router)#network 0.0.0.0
Ruijie(config-router)#end
```

本例用 `network 0.0.0.0` 来指定关联所有直连的网络，这样就无需再逐个指定各个接口上的网络了。

