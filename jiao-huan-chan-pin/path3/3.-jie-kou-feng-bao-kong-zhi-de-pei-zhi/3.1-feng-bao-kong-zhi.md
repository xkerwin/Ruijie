# 3.1 风暴控制

如果网络中出现过量的广播、组播和未知名单播包时，就可能发生了风暴，它会导致网络变慢，正常的网络活动难以进行。

风暴控制采用流控制机制解决风暴。当某一类数据包过量时，交换机会暂时禁止该类数据包的转发，直至数据流恢复正常。

S35系列交换机的接口支持风暴控制设置，它把百兆接口每8个组成一个单位，共享风暴控制的设置。

S3550-24交换机包含3个单位：1-8，9-16，17-24；S3550-48交换机包含6个单位：1-8，9-16，17-24，25-32，33-40，41-48。

当一个接口配置了风暴控制时，其它7个接口也会自动配置上。如果8个接口中的一个变为Aggregate Port成员时，需要对其它接口重新配置，以免配置失效。

## 1、配置风暴控制功能：

## 命令：

```java
Switch(config)#interface interface-id
Switch(config-if)#storm-control level level
Switch(config-if)#storm-control broadcase
Switch(config-if)#storm-control multicast
Switch(config-if)#storm-control unicast
```

`interface` 命令用于指定要配置的接口。

`storm-control level` 命令用于指定风暴控制级别。它的参数level是一个百分数，取值范围是1~100。它表示接口允许某类数据包的最大流量占接口最大带宽的百分比，当流量超过这个百分比时说明风暴发生，接口将丢弃超出部分的此类数据包。缺省值是100。

`storm-control broadcase` 命令用于开启广播风暴的控制功能。

`storm-control multicast` 命令用于开启组播风暴的控制功能。

`storm-control unicast` 命令用于开启对未知名单播风暴的控制功能。

## 说明：

风暴控制级别的值不应该设置太小。3种风暴控制功能不一定全部开启，应根据网络环境适当开启。

## 2、关闭风暴控制功能：

## 命令：

```java
Switch(config)#interface interface-id
Switch(config-if)#no storm-control broadcase
Switch(config-if)#no storm-control multicast
Switch(config-if)#no storm-control unicast
```

## 配置举例：

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#storm-control level 20
Switch(config-if)#storm-control broadcase
Switch(config-if)#storm-control multicast
Switch(config-if)#end
Switch#
```

本例在f0/1口上启用了广播和组播的风暴控制功能，限制广播或组播的流量不能超过最大带宽的20%。同时f0/2~f0/8也都启用了该风暴控制功能。

