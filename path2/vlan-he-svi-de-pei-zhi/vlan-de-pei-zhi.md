# 7.1 VLAN的配置

VLAN是一个2层接口组成的集合，它具有以下特性：

1. 每个VLAN可包含多个2层口，其中可以有Access接口，也可以有Trunk接口。
2. 每个Access接口只能属于一个VLAN（默认是VLAN1），它只能转发属于同一个VLAN的帧。
3. Trunk接口可同时属于多个VLAN（默认是所有VLAN），它可以转发属于不同VLAN的帧。
4. 每个VLAN用一个整数标识，称为VLAN ID，取值范围为1~1007（有些交换机的取值范围可以更大）。
5. 初始时，交换机已经定义了一个ID为1的VLAN，所有物理接口默认属于这个VLAN。

   属于同一个VLAN的接口可以相互通信，属于不同VLAN的接口间不能通信。

## 1、创建VLAN：

```java
Switch(config)#vlan vlan-id
Switch(config-vlan)#name vlan-name
```

`vlan` 命令用于指定一个VLAN，如果指定的VLAN不存在，则创建这个VLAN。

`name` 命令用于给VLAN定义一个名字。如果没有这一步，系统会自动命名为 VLAN xxxx，其中 xxxx 是以0开头的4位VLAN ID号。

## 说明：

创建VLAN的过程可以没有，你可以在添加接口时创建VLAN。

## 2、向VLAN中添加Access接口：

```java
Switch(config)#interface port-id
Switch(config-if)#switchport access vlan vlan-id
```

`interface` 命令用于指定一个接口，这个接口只能是物理接口。

`switchport` 命令用于把该接口分配给指定的VLAN。如果指定的VLAN不存在，则创建这个VLAN。

## 说明：

添加多个接口时，可反复使用上面的过程。

## 3、删除VLAN：

```java
Switch(config)#no vlan vlan-id
```

## 说明：

VLAN 1不能删除。

## 4、查看VLAN：

```java
Switch#show vlan
```

## 配置举例：

定义一个ID为20的VLAN，并把FastEthernet0/1和FastEthernet0/2指派给这个VLAN。

```java
Switch>enable
Switch#configure terminal
Switch(config)#vlan 20
Switch(config-vlan)#name VLAN20
Switch(config-vlan)#exit
Switch(config)#interface f0/1
Switch(config-if)#switchport access vlan 20
Switch(config-if)#interface f0/2
Switch(config-if)#switchport access vlan 20
Switch(config-if)#end
Switch#
```

