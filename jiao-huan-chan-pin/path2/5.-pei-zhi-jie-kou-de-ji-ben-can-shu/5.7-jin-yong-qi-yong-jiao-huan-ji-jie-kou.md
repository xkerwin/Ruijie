# 5.7 禁用/启用交换机接口

交换机的所有接口默认是启用的，此时接口的状态为Up。如果禁用了一个接口，则该接口不能收发任何帧，此时接口的状态为Down。

## 模式：

在接口配置模式中配置。

禁用指定接口：

```java
Switch(config)#interface port-ID

Switch(config-if)#shutdown
```

启用指定接口：

```java
Switch(config)#interface port-ID

Switch(config-if)#no shutdown
```

## 说明：

interface指定的接口可以是物理接口、VLAN或`Aggregate Port`接口。

## 配置举例：禁用交换机的`fastethernet0/1`口。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#shutdown
Switch(config-if)#end
Switch#
```

