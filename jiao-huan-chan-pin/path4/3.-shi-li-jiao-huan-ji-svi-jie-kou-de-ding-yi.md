# 3. 实例----交换机SVI接口的定义

把交换机的F0/1~F0/3定义为一个3层SVI接口，IP地址为192.168.1.1/24。把F0/10定义为一个3层路由口，IP地址为192.168.2.1/24。

## 配置交换机：

```java
Switch>enable
Switch#configure terminal

#创建一个和SVI对应的VLAN
Switch(config)#vlan 2
Switch(config-vlan)#name VLAN2
Switch(config-vlan)#exit

#把F0/1~F0/3指派给VLAN2
Switch(config)#interface f0/1
Switch(config-if)#switchport access vlan 2
Switch(config-if)#interface f0/2
Switch(config-if)#switchport access vlan 2
Switch(config-if)#interface f0/3
Switch(config-if)#switchport access vlan 2

#为VLAN2配置IP地址，使它成为一个3层SVI接口
Switch(config-if)#interface vlan 2
Switch(config-if)#ip address 192.168.1.1 255.255.255.0
Switch(config-if)#no shutdown

#把F0/10配置为3层路由口
Switch(config-if)#interface f0/10
Switch(config-if)#no switchport
Switch(config-if)#ip address 192.168.2.1 255.255.255.0
Switch(config-if)#exit

#启用IP路由
Switch(config)#ip routing
Switch(config)#exit

#查看配置结果
Switch#show vlan
Switch#show running-config
Switch#show ip route

#保存配置
Switch#copy running-config startup-config
```

说明：

SVI是一种和VLAN相对应的3层口，你只需要给VLAN配置一个IP地址就成了SVI接口。

SVI是一种由多个物理接口组成的3层口，用它们连接的计算机构成一个网段，比如图中的PC1、PC2、PC3与SVI在同一个网段中，彼此可以共享资源。

在实际应用中，SVI多用做交换机的管理接口，你也可以通过SVI使处于不同网段的VLAN可以通信。

## 效果验证：

PC1、PC2、PC3彼此间可以通信，也能通过“网上邻居”共享文件。它们和PC4可以通信，但不能通过“网上邻居”共享文件。

四：实例----交换机通道口的配置

两台交换机之间通过F0/10~F0/12互联，把它们定义为Aggregate Port接口，使之成为两个交换机间的高速通道。

## 配置交换机S1：

```java
S1>enable
S1#configure terminal

#把F0/10~F0/12加入到同一个Aggregate Port接口组中
S1(config)#interface f0/10
S1(config-if)#port-group 2
S1(config-if)#interface f0/11
S1(config-if)#port-group 2
S1(config-if)#interface f0/12
S1(config-if)#port-group 2
S1(config-if)#end

#查看配置结果
S1#show aggregateport 2
S1#show running-config

#保存配置
S1#copy running-config startup-config
```

## 配置交换机S2：

```java
S2>enable
S2#configure terminal

#把F0/10~F0/12加入到同一个Aggregate Port接口组中
S2(config)#interface f0/10
S2(config-if)#port-group 2
S2(config-if)#interface f0/11
S2(config-if)#port-group 2
S2(config-if)#interface f0/12
S2(config-if)#port-group 2
S2(config-if)#end

#查看配置结果
S2#show aggregateport 2
S2#show running-config

#保存配置
S2#copy running-config startup-config
```

## 说明：

`Aggregate Port`接口用于构建交换机之间的高速通道，它的速率是组成它的各个接口速率之和。

`Aggregate Port`接口由多个物理接口组成，接口用一个ID号标识（本例为2），使用 port-group 命令可以向其中添加接口。

不同型号的交换机对`Aggregate Port`接口的支持不同，在锐捷的3550系列交换机中：

S3550-24交换机最大支持6个AP，每个AP最多包含8个接口，其中6号AP只为模块1和模块2保留；

S3550-48交换机不支持AP；

S3550-12G、S3550-24G交换机最大支持12个AP，每个AP最多包含8个接口；

S3550-12SFP/GT交换机最大支持12个AP，每个AP最多包含8个接口。

如果需要配置3层Aggregate Port，可以在配置中增加以下内容：

```java
S1(config)#interface aggregateport 2
S1(config-if)#no switchport
S1(config-if)#ip address 192.168.1.1 255.255.255.0
```

这样交换机S1的AP2就成为一个3层口，它连接了一个地址为192.168.1.0/24的网段。

