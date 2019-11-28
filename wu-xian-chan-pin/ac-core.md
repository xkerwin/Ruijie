# AC旁挂核心配置（AC-核心）

### 一、需求：

* AP地址池在核心上 `10.10.10.1/24` 网关：`10.10.10.254/24` `vlan10`
* 无线用户地址池在核心上 `192.18.0.1/24` 网关：`192.18.0.254/24` `vlan20`

#### AC配置

```text
---AP上线配置---

Ruijie>enable
//进入特权模式

Ruijie#configure terminal
//进入全局配置模式

Ruijie(config)#int loopback 0
Ruijie(config-if-Loopback 0)#ip address 1.1.1.1/24 
Ruijie(config-if-Loopback 0)#exit
//配置该ip地址用于与AP建立capwap隧道

Ruijie(config)#int vlan10
Ruijie(config-int-vlan)#ip add 10.10.10.1/24
Ruijie(config-int-vlan)#exit
//创建与核心互联vlan

Ruijie(config)#ip route 0.0.0.0 0.0.0.0 10.10.10.254
//配置全局路由指向核心vlan10地址

Ruijie(config)#int gigabitEthernet 0/8
//AC和核心互连端口trunk配置

Ruijie(config-if-GigabitEthernet 0/8)#switchport mode trunk
//进入到g0/8口（与核心互联端口）

Ruijie(config-if-GigabitEthernet 0/8)#exit
//将该接口配置成trunk端口

Ruijie(config)#end
//结束配置

Ruijie#wr
//保存配置
```

#### 核心上配置：

```text
AP网关和dhcp配置

Ruijie(config)#vlan  10
//创建ap管理vlan 10

Ruijie(config-vlan)#exit
Ruijie(config)#interface vlan 10
Ruijie(config-int-vlan)#ip add 10.10.10.254/24
Ruijie(config-int-vlan)#exit
//该地址做为ap的网关地址

Ruijie(config)#service dhcp
//开启DHCP服务

Ruijie(config)#ip dhcp pool ap_ruijie
//创建AP设备DHCP地址池，名称是ap_ruijie

Ruijie(config-dhcp)#option 138 ip 1.1.1.1
//配置option字段，指定AC的地址，即AC的loopback 0地址

Ruijie(config-dhcp)#network 10.10.10.0/24
//分配给ap的地址

Ruijie(config-dhcp)#default-route 10.10.10.254
//分配给ap的网关地址

Ruijie(config-dhcp)#exit
//退出DHCP配置

Ruijie(config)#ip route 1.1.1.1 255.255.255.255 10.10.10.1
//配置option路由指向AC网关

Ruijie(config)#ip dhcp pool ap_wifi
//创建wifi用户DHCP地址池，名称是ap_wifi

Ruijie(config-dhcp)#network 192.18.0.0/24
//分配给wifi用户的地址

Ruijie(config-dhcp)#default-route 192.18.0.254
//分配给wifi用户的网关地址

Ruijie(config-dhcp)#exit
//退出DHCP配置

Ruijie(config)#interface range g0/1-24
Ruijie(config-if-range)#switchport mode trunk
//配置下联AP/接入交换机端口

Ruijie(config-if-range)#switchport trunk native vlan 10
//注意：AP没有使用vlan1，则需要将对应的vlan改为native vlan（本征vlan）

Ruijie(config-if-range)#exit
//退出接口配置

Ruijie(config)#interface g0/1
Ruijie(config-if-GigabitEthernet 0/1)#switchport mode trunk
//核心和AC互连端口trunk配置

Ruijie(config-if-GigabitEthernet 0/1)#switchport trunk allowed vlan only 10,20
//vlan裁剪，放通所需vlan

Ruijie(config-if-GigabitEthernet 0/1)#exit
//退出接口配置

Ruijie(config)#end
//结束配置

Ruijie#wr
//保存配置
```

#### 检验：

* AP/PC能在核心/接入交换机上正常获取到 `vlan10`地址

