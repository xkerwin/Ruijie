# 10.2 RIP协议参数的配置

通常情况下，我们让RIP协议的各项参数取默认值就行了，无需进行配置，如果需要的话可以用命令修改它们的值，修改时应该先用router rip 命令进入RIP的配置模式。

## 1、配置默认跳数：

```java
Ruijie(config-router)#default-metric number
```

默认跳数是指访问本地网络的花费（跳数）。它的取值范围为1~15，缺省值为1。

## 2、配置计时器：

```java
Ruijie(config-router)#timers basic update invalid holddown
```

`update：`更新时间。是发送更新报文的时间间隔。默认为30秒，有效取值范围是0~2147483647。

`invalid：`失效时间。是宣布无效的时间间隔。默认为180秒，有效取值范围是1~2147483647。

holddown：清除时间。是对失效项目保持的时间。默认为120秒，有效取值范围是0~2147483647。

## 3、配置邻居：

```java
Ruijie(config-router)#neighbor ip-address
```

RIP协议是用广播发布路由更新的，设置邻居可以使RIP和非广播网络的路由器交换路由信息。命令中的ip-address是邻居路由器的地址。

## 4、设置RIP版本：

```java
Ruijie(config-router)#version version-number
```

`version-number`的取值为1或2。默认情况下，RIP协议可接收RIPv1和RIPv2的报文，发送RIPv1的报文。用 version 1 命令可设置为仅发送和接收RIPv1的报文，用 version 2 命令可设置为仅发送和接收RIPv2的报文。另外，你也可以用 `ip rip send|receive version` 命令设置各个接口发送和接收的版本。

