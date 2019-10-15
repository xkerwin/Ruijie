# 5.4 配置接口描述

接口描述常用于标注一个接口的功能、用途等，有利于记录和了解网络拓扑。

## 模式：

在接口配置模式中配置。

## 配置命令：

```java
Ruijie(config)#interface interface-ID
Ruijie(config-if)#description string
```

`interface`命令用于指定要配置的接口。参数interface-ID是接口的类型和编号。

`description`命令用于设置此接口的描述文字。

## 说明：

接口描述的文字最多不得超过32个字符。

## 删除配置的描述：

```java
Ruijie(config)#interface interface-ID
Ruijie(config-if)#no description
```

## 配置举例：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#interface f0/1
Ruijie(config-if)#description to-PC1
Ruijie(config-if)#interface f0/2
Ruijie(config-if)#description to-Switch1
Ruijie(config-if)#end
Ruijie#
```

本例为`fastethernet0/1`和`fastethernet0/2`配置了接口描述，这样可方便了解它们所连接的设备。

配置的接口描述可以在配置文件中看到。

