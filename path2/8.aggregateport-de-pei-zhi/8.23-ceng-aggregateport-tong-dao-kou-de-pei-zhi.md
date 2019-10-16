# 8.2 3层Aggregate Port（通道口）的配置

3层Aggregate Port和2层Aggregate Port的区别在于3层Aggregate Port具有IP地址，可作为网关连接一个子网。

配置3层Aggregate Port时，可以先创建一个3层Aggregate Port，再向其中加入成员接口，也可以先配置一个2层Aggregate Port，再把它定义为3层口。

## 定义3层Aggregate Port：

```java
Switch(config)#interface aggregateport AP-id
Switch(config-if)#no switchport
Switch(config-if)#ip address IP-address Subnet-Mask
```

`interface aggregateport` 命令用于指定一个Aggregate接口，如果指定的Aggregate接口还不存在，则创建该接口。

`no switchport` 命令用于把该接口转换为3层口。

`ip address` 命令用于给这个3层Aggregate Port设置IP地址和子网掩码。

## 配置举例：

把交换机的FastEthernet0/4和FastEthernet0/5组成一个3层Aggregate接口。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface aggregateport 1
Switch(config-if)#no switchport
Switch(config-if)#ip address 192.168.8.1 255.255.255.0
Switch(config-if)#interface f0/4
Switch(config-if)#port-group 1
Switch(config-if)#interface f0/5
Switch(config-if)#port-group 1
Switch(config-if)#end
Switch#
```

