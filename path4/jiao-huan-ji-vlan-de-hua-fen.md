# 2. 实例----交换机VLAN的划分

两台S3550-12交换机利用VLAN分割了几个虚拟局域网，使用时属于同一个VLAN的计算机之间可以通信，属于不同VLAN的计算机之间不能通信。

## 配置S1：

```java
S1>enable
S1#configure terminal

#创建VLAN20
S1(config)#vlan 20
S1(config-vlan)#name VLAN20

#创建VLAN30
S1(config-vlan)#vlan 30
S1(config-vlan)#name VLAN30
S1(config-vlan)#exit

#把F0/4~F0/7指派给VLAN20
S1(config)#interface f0/4
S1(config-if)#switchport access vlan 20
S1(config-if)#interface f0/5
S1(config-if)#switchport access vlan 20
S1(config-if)#interface f0/6
S1(config-if)#switchport access vlan 20
S1(config-if)#interface f0/7
S1(config-if)#switchport access vlan 20

#把F0/8~F0/11指派给VLAN30
S1(config-if)#interface f0/8
S1(config-if)#switchport access vlan 30
S1(config-if)#interface f0/9
S1(config-if)#switchport access vlan 30
S1(config-if)#interface f0/10
S1(config-if)#switchport access vlan 30
S1(config-if)#interface f0/11
S1(config-if)#switchport access vlan 30

#把F0/12配置为Trunk模式
S1(config-if)#interface f0/12
S1(config-if)#switchport mode trunk
S1(config-if)#end

#查看配置结果
S1#show vlan

#保存配置
S1#copy running-config startup-config
```

## 配置S2：

```java
S2>enable
S2#configure terminal

#创建VLAN30
S2(config)#vlan 30
S2(config-vlan)#name VLAN30
S2(config-vlan)#exit

#把F0/1~F0/5指派给VLAN30
S2(config)#interface range f0/1-5
S2(config-if)#switchport access vlan 30

#把F0/12配置为Trunk模式
S2(config-if)#interface f0/12
S2(config-if)#switchport mode trunk
S2(config-if)#end

#查看配置结果
S2#show vlan

#保存配置
S2#copy running-config startup-config
```

## 说明：

为了简化配置过程，在配置S2时采用了接口组的配置方式，你也可以在S1中使用此方法。

加入VLAN的接口必须是`Access`口，你可以添加 `switchport mode access` 命令来保证这一点。

创建VLAN的过程可以没有，当你把一个接口加入一个不存在的VLAN时，交换机会自动创建此VLAN。

所有未指派的接口默认属于VLAN1。

## 效果验证：

在交换机上连接计算机，连接在同一个VLAN上的计算机间可以通信，而连接在不同VLAN上的计算机间不能通信。

