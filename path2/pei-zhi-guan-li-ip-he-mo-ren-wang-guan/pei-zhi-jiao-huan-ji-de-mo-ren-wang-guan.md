# 3.2 配置交换机的默认网关

当交换机接收到一个不知该发往何处的数据报时，就把该数据报发往默认网关。

只有2层设备才需要配置默认网关，3层设备是通过配置路由把数据报发送出去的。

## 模式：

在全局配置模式中配置。

## 配置命令：

```java
Ruijie(config)#ip default-gateway IP-address
```

`IP-address`是默认网关的IP地址。

## 删除配置的默认网关：

```java
Ruijie(config)#no ip default-gateway
```

## 配置举例：

配置交换机的默认网关为192.168.1.1。

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#ip default-gateway 192.168.1.1
Ruijie(config)#end
Ruijie#
```

配置的默认网关可以在配置文件中看到。

