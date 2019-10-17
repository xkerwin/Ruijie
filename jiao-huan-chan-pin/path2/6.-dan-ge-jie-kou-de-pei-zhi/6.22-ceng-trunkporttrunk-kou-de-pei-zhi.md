# 6.2 2层Trunk Port（Trunk口）的配置

交换机的接口默认是Access接口，此时它只能转发来自同一个VLAN的帧，如果需要让它能够转发不同VLAN的帧，需要设置为Trunk接口。

通常我们需要把交换机和交换机、交换机和路由器连接的接口设置为Trunk接口。

## 1、把接口配置为Trunk接口：

Switch\(config\)\#interface port-id

```java
Switch(config-if)#switchport mode trunk
interface 命令用于指定要修改的接口，这个接口只能是物理接口。
switchport mode trunk 命令用于把该接口设置为Trunk Port。
```

## 2、恢复Trunk接口为Access接口：

```java
Switch(config)#interface port-id
Switch(config-if)#switchport mode access
```

## 说明：

也可以使用 no switchport mode 命令把接口模式恢复为默认值，而默认值就是Access Port。

## 配置举例：

配置交换机的FastEthernet0/1为Trunk接口。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface f0/1
Switch(config-if)#switchport mode trunk
Switch(config-if)#end
Switch#
```

