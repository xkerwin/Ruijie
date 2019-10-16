# 3.2 查看风暴控制信息

## 模式：

特权模式。

## 命令：

```java
Switch#show storm-control interface-id
```

`interface-id`是可选的，用于查看指定接口的风暴控制信息。如：

```java
Switch#show storm-control

interface　　　Broadcase　　Multicast　　Unicast　　　Level

---------　　　---------　　---------　　-------　　--------

Fa0/1　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/2　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/3　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/4　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/5　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/6　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/7　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/8　　　　　Enable　　　　Enable　　　Disable　　　20%
Fa0/9　　　　　Disable　　　 Disable　　 Disable　　　100%
Fa0/10　　　　 Disable　　　 Disable　　 Disable　　　100%
Fa0/11　　　　 Disable　　　 Disable　　 Disable　　　100%
Fa0/12　　　　 Disable　　　 Disable　　 Disable　　　100%
......
```

各个栏目依次为：接口、Broadcase\(广播风暴\)、Multicast\(组播风暴\)、Unicast\(未知名单播风暴\)、控制级别。

`Enable`表示开启，`Disable`表示关闭。

