# 端口防环路RLDP功能介绍及配置

**应用场景：**

RLDP功能主要是应用到接入层交换机上做环路检测用（汇聚层也可以开RLDP防环，但是控制防范的粒度比较粗糙），特别适用于交换机下联HUB上面自身打环的情况（BPDUGUARD无法实现防止这类的环路），所以我们推荐在项目实施的时候接入层交换机的各个接终端用户的端口都开启RLDP，作为一个优化配置进行事先部署，防止端口下的各类环路问题。

**功能简介：**

**RLDP：**RLDP全称是Rapid Link Detection Protocol，是锐捷网络自主开发的一个用于快速检测以太网链路故障的链路协议。

一般的以太网链路检测机制都只是利用物理连接的状态，通过物理层的自动协商来检测链路的连通性。但是这种检测机制存在一定的局限性，在一些情况下无法为用户提供可靠的链路检测信息，比如在光纤口上光纤接收线对接错，由于光纤转换器的存在，造成设备对应端口物理上是linkup的，但实际对应的二层链路却是无法通讯的。再比如两台以太网设备之间架设着一个中间网络，由于网络传输中继设备的存在，如果这些中继设备出现故障，将造成同样的问题。

**BPDU Guard：**BPDU Guard即BPDU防护，如果该端口配置了BPDU Guard功能，如果该端口收到了BPDU报文，就进入Error-disabled 状态，无法转发数据

网络中一般二层环路有如下几种常见的情形：

**情形一：**三角环路\(两台核心都连接同一台接入\)

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1ae80408_0.png)

对于这种环路情形，可以通过在三台交换机之间运行MSTP实现环路切换与线路冗余，具体可以参见典型应用场景中“MSTP+VRRP+FW”部分相关章节

**情形二：**核心两根线都连接到同一台接入交换机

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1aed0409_0.png)

对于这种环路情形可以通过在核心交换机和接入交换机上配置二层链路聚合来实现链路冗余，具体可以参见端口聚合章节

**情形三：**同一根线的头尾两端都插到交换机的两个端口

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1af2040a_0.png)

对于防止这种网络环路，可以通过RLDP或BPDU Guard功能实现

**情形四：**接入交换机连接傻瓜式交换机，傻瓜式交换机上的两个端口环路

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1af7040b_0.png)

对于这种网络场景建议通过RLDP功能来实现

**说明：**对于场景四的防环，由于部分HUB会过滤BPDU报文的特性，不能通过BPDU Guard功能实现，因为端口发出的BPDU报文，目的MAC地址是公有的MAC地址01-80-C2-00-00-00，市场上部分傻瓜式交换机（如TP-Link或D-Link等）会丢弃这种公有标准的组播报文，无法转发，所以即使傻瓜式交换机出现了环路，也不会把BPDU报文转发回交换机，交换机也就无法把该端口置为err-disable。但是对于RLDP报文是我司私有的报文，目的组播mac为01-d0-f8-00-00-02，傻瓜式交换机能转发这样的组播报文，故能检测环路

**一、组网需求**

为了防止接入交换机下联的端口出现环路（交换机本身的环路（情形三场景）及下联HUB出现的环路（情形四场景）），需要在交换机上配置RLDP功能

**二、配置要点**

1、全局开启RLDP功能

2、接口下开启RLDP功能，并且设置环路后的处理方式

3、设置接口自动恢复时间

**三、组网拓扑**

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1afc040c_0.png)

**四、配置步骤**  

接入交换机配置如下：

```text
Ruijie>en

Rujijie#configure terminal

Rujijie(config)#rldp enable   
//全局开启RLDP功能

Rujijie(config)#interface range g0/1-24    
//对于下联PC或HUB的端口需要开启，不要在接入交换机的上联口开启该功能

Rujijie(config-if-range)#rldp port loop-detect shutdown-port 
//接口开启RLDP功能，如果检测出环路后shutdow该端口

Rujijie(config-if-range)#exit

Rujijie(config)#errdisable recovery interval 300    
//如果端口被RLDP检测并shutdown，再过300秒后会自动恢复，重新检测是否有环路

Rujijie(config)#end

Rujijie#wr
```

**说明：**

1）建议在接入下联端口开启RLDP功能的同时，也同时开启BPDUGuard+Portfast功能（需要注意该功能生效，必须要先开启STP协议），如果网络中没有运行生成树协议（单核心网络环境），可以在接入交换机上开启STP功能，同时上联口开启BPDUFilter，防止STP报文发送到核心交换机，影响整网。命令如下：

```text
Ruijie>en

Rujijie#configure terminal

Ruijie(config)#spanning-tree

Ruijie(config)#interface range g0/1-24

Ruijie(config-if-range)#spanning-tree bpduguard enable

Ruijie(config-if-range)#spanning-tree portfast

Ruijie(config)#interface gigabitEthernet 0/25

Ruijie(config-if-GigabitEthernet 0/25)#spanning-tree bpdufilter enable

Ruijie(config-if-GigabitEthernet 0/25)#exit

Rujijie(config)#errdisable recovery interval 300

Rujijie(config)#end

Rujijie#wr
```

**五、功能验证**

1、查看RLDP的状态

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1b01040d_0.png)

2、当g0/5和g0/7口环起来后会出现如下log

```text
Rujijie#
*Mar 19 20:16:00: %RLDP-3-LINK_DETECT_ERROR: loop detection error detect on interface GigabitEthernet 0/7.set this interface errordisable!
*Mar 19 20:16:00: %RLDP-3-LINK_DETECT_ERROR: loop detection error detect on interface GigabitEthernet 0/5.set this interface errordisable!
*Mar 19 20:16:01: %LINEPROTO-5-UPDOWN: Line protocol on Interface VLAN 1, changed state to down.
*Mar 19 20:16:02: %LINK-3-UPDOWN: Interface GigabitEthernet 0/5, changed state to down.
*Mar 19 20:16:02: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet 0/5, changed state to down.
*Mar 19 20:16:02: %LINK-3-UPDOWN: Interface GigabitEthernet 0/7, changed state to down.
*Mar 19 20:16:02: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet 0/7, changed state to down.
```

3、查看接口状态，发现这两个口被disable了

![](https://yixiu.ruijie.com.cn:8902/ueditor/jsp/upload/image/move_20180918/exchange/4a607e64-6d2b-4f1f-bea5-56f60f62c61f_files/97691069_1b06040e_0.png)

4、过了300S，交换机会把端口自动变为恢复状态，如下：

```text
*Mar 19 20:21:01: %PORT_SECURITY-4-ERR_RECOVER: Interface GigabitEthernet 0/5 recover from an error.
*Mar 19 20:21:01: %PORT_SECURITY-4-ERR_RECOVER: Interface GigabitEthernet 0/7 recover from an error.
*Mar 19 20:21:01: %RLDP-3-LINK_DETECT_RECOVER: rldp recover interface GigabitEthernet 0/7 from loop error
*Mar 19 20:21:01: %RLDP-3-LINK_DETECT_RECOVER: rldp recover interface GigabitEthernet 0/5 from loop error
*Mar 19 20:21:04: %LINEPROTO-5-UPDOWN: Line protocol on Interface VLAN 1, changed state to up.
*Mar 19 20:21:06: %LINK-3-UPDOWN: Interface GigabitEthernet 0/5, changed state to up.
*Mar 19 20:21:06: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet 0/5, changed state to up.
*Mar 19 20:21:06: %LINK-3-UPDOWN: Interface GigabitEthernet 0/7, changed state to up.
*Mar 19 20:21:06: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet 0/7, changed state to up.
```

5、如果需要立即恢复被disable的端口，可以通过如下命令实现;

```text
Rujijie#rldp reset
Rujijie#
*Mar 19 20:34:32: %PORT_SECURITY-4-ERR_RECOVER: Interface GigabitEthernet 0/7 recover from an error.
*Mar 19 20:34:32: %RLDP-3-LINK_DETECT_RECOVER: rldp recover interface GigabitEthernet 0/7 from loop error
*Mar 19 20:34:32: %PORT_SECURITY-4-ERR_RECOVER: Interface GigabitEthernet 0/5 recover from an error.
*Mar 19 20:34:32: %RLDP-3-LINK_DETECT_RECOVER: rldp recover interface GigabitEthernet 0/5 from loop error
```

