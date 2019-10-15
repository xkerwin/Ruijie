# 5.5 配置接口速率

S3550的接口都是具有多种速率的自适应接口，`FastEthernet`接口有10/100M两种速率，`GigabitEthernet`接口有10/100/1000M三种速率，默认情况下，他们用自协商方式确定他的工作速率。用配置可指定他们只使用某一个固定速率。

## 模式：

在接口配置模式中配置。

## 配置命令：

```java
Switch(config)#interface port-ID
Switch(config-if)#speed 10 | 100 | 1000 | auto
```

`interface` 命令用于指定要配置的接口。指定的接口可以是物理接口或`Aggregate Port`接口。

speed 命令用于设置此接口的速率。

## 参数：

10——10Mbps，100——100Mbps，1000——1000Mbps（只能用于GigabitEthernet接口），auto——使用自协商模式（默认值）。

## 说明：

当接口速率不是auto时，自协商过程被关闭，此时要求与该接口相连的设备必须支持此速率。

## 删除配置的速率：

```java
Switch(config)#interface port-ID

Switch(config-if)#no speed
```

删除配置的速率后，此接口的速率默认为auto。

## 配置举例：

配置交换机的`fastethernet0/1`口速率为100Mbps。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#speed 100
Switch(config-if)#end
Switch#
```

配置的接口速率可以在配置文件中看到。

