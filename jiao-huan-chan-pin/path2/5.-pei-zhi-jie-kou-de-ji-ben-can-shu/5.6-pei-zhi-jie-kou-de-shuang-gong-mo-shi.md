# 5.6 配置接口的双工模式

S3550的接口可工作于半双工模式或全双工模式，默认情况下，他们用自协商方式确定他的双工模式。用配置可指定他们只使用某一种双工模式。

## 模式：

在接口配置模式中配置。

## 配置命令：

```java
Switch(config)#interface port-ID
Switch(config-if)#duplex auto | half | full
```

`interface` 命令用于指定要配置的接口。指定的接口可以是物理接口或`Aggregate Port`接口。

`duplex` 命令用于设置此接口的双工模式。

## 参数：

auto——使用自协商模式（默认值），half——半双工模式，full——全双工模式。

## 说明：

当双工模式不是auto时，自协商过程被关闭，此时要求与该接口相连的设备必须支持此双工模式。

## 删除配置的双工模式：

```java
Switch(config)#interface port-ID
Switch(config-if)#no duplex
```

删除配置的双工模式后，此接口的双工模式默认为auto。

## 配置举例：

配置交换机的`fastethernet0/1`口双工模式为全双工模式。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#duplex full
Switch(config-if)#end
Switch#
```

配置的接口双工模式可以在配置文件中看到。

