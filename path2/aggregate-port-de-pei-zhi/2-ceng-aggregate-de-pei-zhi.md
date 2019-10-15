# 8.1 2层Aggregate Port（通道口）的配置

当两台交换机互联时，为了提高连接的带宽，可以使用多个接口进行互联，这时需要把这些接口设置为Aggregate接口。

Aggregate Port具有以下特性：

1. 从物理上看，Aggregate接口是由多个物理接口组成的，但在逻辑上，我们可把它理解为一个高速接口，它的带宽是组成它的各接口带宽之和。
2. 组成Aggregate口的物理接口必须是同类接口，接口参数也必须相同，同属于一个VLAN。
3. 一个Aggregate口包含的物理接口数量一般不能超过8个。
4. Aggregate口具有流量平衡功能，当其中一条成员链路断开时，系统会自动把它的流量分配到其它有效链路上，不影响该接口的使用。
5. 每个Aggregate接口用一个整数标识，称为AP ID，取值范围为1~12。

## 1、创建Aggregate口：

```java
Switch(config)#interface port-id
Switch(config-if)#port-group AP-id
```

`interface` 命令用于指定要加入Aggregate的接口，这个接口只能是物理接口。

`port-group` 命令用于把该接口加入到指定的Aggregate中。AP-id是Aggregate接口的编号，取值为1~12。如果指定的Aggregate接口还不存在，则创建该接口。

## 说明：

重复上面的操作，可以向Aggregate口添加多个接口。

## 2、从Aggregate中删除接口：

```java
Switch(config)#interface port-ID
Switch(config-if)#no port-group
```

## 3、查看Aggregate接口：

```java
Switch#show aggregateport AP-id
```

## 配置举例：

把交换机的FastEthernet0/4和FastEthernet0/5组成一个Aggregate接口。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/4
Switch(config-if)#port-group 1
Switch(config-if)#interface f0/5
Switch(config-if)#port-group 1
Switch(config-if)#end
Switch#
```

