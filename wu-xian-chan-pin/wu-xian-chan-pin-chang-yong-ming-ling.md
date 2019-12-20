# 无线产品常用命令

### 1. AC常见维护命令

#### 1.1 查看AC与AP建立隧道的情况

```cpp
Ruijie#show capwap state
CAPWAP tunnel state, 2 peers, 2 is run:
Index     Peer IP              Port      State         Mac Address
1         192.168.0.121        10000     Run           0074.9ce9.e0bc
2         192.168.0.120        10000     Run           8005.889f.3dd9
                                        "Run为成功关联状态"
```

#### 1.2 查看AP的配置

```cpp
Ruijie#show ap-config running
Building configuration...
Current configuration: 535 bytes
!
ap-config 8005.889f.3dc1
   ap-mac 8005.889f.3dc1
!
ap-config "AP名称"
 ap-mac 8005.889f.3dc1 //对应AP的设备标签贴的mac地址，也是show ap-con su 的mac地址，这个命令是自动识别生成的
 ap-group "AP组名"
 location "位置信息"
 country US  radio 1 //所在国家（2.4G）
 power local 100 radio 1 //2.4G信号功率%
 power local 100 radio 2 //5G信号功率%
 coverage-area-control 12 radio 1 //2.4G配置管理帧发送功率（此参数单位为db）
 coverage-area-control 17 radio 2 //5G配置管理帧发送功率（此参数单位为db） 
 response-rssi 20 radio 1 //2.4G配置无线用户接入最小RSSI值（终端接入无线时的最低rssi）
 response-rssi 20 radio 2 //5G配置无线用户接入最小RSSI值（终端接入无线时的最低rssi）
 channel 1 radio 1 //2.4G无线信道
 channel 153 radio 2 //5G无线信道
 chan-width 40 radio 1 //2.4G无线频率带宽(Mhz)
 chan-width 40 radio 2 //5G无线频率带宽(Mhz)
```

#### 1.3 查看特定AP的配置

```cpp
Ruijie#show ap-config running "AP名称"
Building configuration...
Current configuration: 243 bytes
!
ap-config "AP名称"
 ap-mac 0074.9ce9.e0bc //对应AP的设备标签贴的mac地址，也是show ap-con su 的mac地址，这个命令是自动识别生成的
 ap-group "AP组名"
 location "位置信息"
 country US  radio 2 //所在国家（5G）
 power local 100 radio 1 //2.4G信号功率%
 power local 100 radio 2 //5G信号功率%
 coverage-area-control 12 radio 1 //2.4G配置管理帧发送功率（此参数单位为db）
 coverage-area-control 17 radio 2 //5G配置管理帧发送功率（此参数单位为db）
 response-rssi 20 radio 1 //2.4G配置无线用户接入最小RSSI值（终端接入无线时的最低rssi）
 response-rssi 20 radio 2 //5G配置无线用户接入最小RSSI值（终端接入无线时的最低rssi）
 channel 1 radio 1 //2.4G无线信道
 channel 153 radio 2 //5G无线信道
 chan-width 40 radio 1 //2.4G无线频率带宽(Mhz)
 chan-width 40 radio 2 //5G无线频率带宽(Mhz)
```

#### 1.4 查看ap工作信道及功率等射频参数

```cpp
Ruijie#show ap-config summary
========= show ap status =========
Radio: Radio ID or Band: 2.4G = 1#, 5G = 2#
       E = enabled"启用", D = disabled"关闭", N = Not exist"不存在", V = Virtual AP"虚拟AP"
       Current Sta number
       Channel: * = Global
       Power Level = Percent

Online AP number: 2 //在线AP数量
Offline AP number: 1 //离线AP数量

AP Name  IP Address    Mac Address     Radio         Radio           Up/Off time   State
-------  ----------    --------------  -----------   -------------   ------------  -----
AP名称    AP IP地址     AP Mac地址      1|E|3|1|100   2|E|5|157|80    41:18:41:16    Run
ruijie   192.168.0.1   8005.889f.3dd9  1 E 3 1 100   1 E 5 157 100   26:03:52:32    Run       
//Radio解析：1/2.4G信号，E/启用，3/Radio用户数，1/Radio工作信道，100/Radio信号功率%
//Radio解析：2/5G信号，E/启用，5/Radio用户数，157/Radio工作信道，80/Radio信号功率%
```

#### 1.5 查看已关联的无线用户

```cpp
Ruijie#show ac-config client  by-ap-name
========= show sta status =========
AP    : ap name/radio id
Status: Speed/Power Save/Work Mode/Roaming State/MU MIMO, E = enable power save, D = disable power save
        BACKUP = STA is on peer AC

Total Sta Num : 17
Backup Sta Num : 0
STA MAC         IPV4 Address   AP     Wlan Vlan Status       Asso Auth  Net Auth  Uptime
--------------  -------------  ------ ---- ---- -----------  ---------- --------  ------
用户MAC          用户IP         AP     Wlan vlan 状态         认证方式              关联时长
0c54.15db.b74e  192.168.0.117  ruijie 1    1    72.5M/D/bgn  WPA2_PSK   OPEN      0:00:41:27
```

#### 1.6 查看已经关联的无线用户的详细信息，mac、ip、vlan、wlan、漫游状态、关联的AP名称和IP等等

```cpp
Ruijie#show ac-config client detail 0c54.15db.b74e
Mac Address         :0c54.15db.b74e
IP Address          :192.168.0.117
Wlan Id             :1
Vlan Id             :1
Roam State          :Local //非漫游，如果是漫游则显示为Roam
Association ID      :6

Associated Ap Information:
AP Name             :"AP名称"
AP IP               :192.168.0.120
```

#### 1.7 查看无线客户端连接状态，认证状态

```cpp
Ruijie#show wlan stainfo summary
total stainfo number: 16 //连接数量
INDEX    MAC-address          WLAN ID  Wireless-state   PTK-state  PMF
-----    -----------          -------  --------------   ---------  ---
序号      客户端Mac地址        无线ID    认证状态          
1        5013.9514.44a3       1        AUTH-and-ASSOC   11         NO
2        5013.95bd.65fc       1        AUTH-and-ASSOC   11         NO
3        001a.34fe.38df       1        AUTH-and-ASSOC   11         NO
4        e076.d046.85b6       1        AUTH-and-ASSOC   11         NO
5        a057.e33b.4c51       1        AUTH-and-ASSOC   11         NO
6        0013.eff6.0b2c       1        AUTH-and-ASSOC   11         NO
7        0c54.15db.b74e       1        AUTH-and-ASSOC   11         NO
8        8844.774a.9584       1        AUTH-and-ASSOC   11         NO
9        2cff.ee82.9613       1        AUTH-and-ASSOC   11         NO
10       503c.eae5.96bf       1        AUTH-and-ASSOC   11         NO
11       9810.e8ba.b51d       1        AUTH-and-ASSOC   11         NO
12       200d.b033.4452       1        AUTH-and-ASSOC   11         NO
13       e0dd.c03e.6982       1        AUTH-and-ASSOC   11         NO
14       cc79.cf66.896c       1        AUTH-and-ASSOC   11         NO
15       60a3.7d6f.5344       1        AUTH-and-ASSOC   11         NO
16       c0a6.0085.65a2       1        AUTH-and-ASSOC   11         NO
```

#### 1.8 查看无线用户的加密方式

```cpp
Ruijie#show wclient security "5013.9514.44a3" //无线客户端MAC地址
Security policy finished      : TRUE //安全策略
Security policy type          : PSK //安全类型
Security WPA version          : WPA2 //加密方式
Security Ucast cipher         : CCMP //Ucast安全码
Security EAP type             : NONE //EAP安全类型
```

#### 1.9 查看无线AC的硬件信息

```cpp
Ruijie#show ac-device information
AC device information:
   CPU type         : MIPS 1004Kc V2.15, 292MHz //CPU信息
  Memory type      : DDR3 //内存信息
  Flash  size      : 1MB //Flash空间
```

#### 1.10 查看已关联到AC上的AP硬件信息

```cpp
Ruijie#show ap-device information
AP(name)s device information:
  CPU type         : MIPS 74Kc V5.0, 386MHz //CPU信息
  Memory type      : Hynix DDR2(16bit) //内存信息
  Flash  size      : 31MB //Flash空间
  Mac Address      : 0074.9ce9.e0bc //MAC地址
```

### 2. AP常见查询命令

#### 2.1 如何查看ap当前的工作模式

```cpp
Ruijie>show ap-mode
current mode: fit //fit是瘦模式，fat是胖模式
```

#### 2.2 如何获取AP设备本身的MAC地址（非物理接口mac）

```cpp
查找AP MAC地址有以下几种方法：
1.AP外壳机身贴纸上可以看到设备的MAC地址
2.在AC上"show version all"或"sho ap-device information"可以看到AP的MAC地址
3.登入AP "show arp"查看物理接口的MAC，一般情况下设备MAC为物理接口MAC减1
```

#### 2.3 AP下如何查看无线客户端

```cpp
Ruijie>show dot11 associations all-client
RADIO-ID WLAN-ID ADDR              AID  CHAN RATE_DOWN RATE_UP RSSI ASSOC_TIME IDLE TXSEQ  RXSEQ  ERP  STATE  CAPS HTCAPS VHT_MU_CAP
-------- ------- ----------------- ---- ---- --------- ------- ---- ---------- ---- -----  -----  ---  -----  ---- ------ ----------
1        1       50:13:95:bd:65:fc 2    1      65.0M     26.0M 30   5:58:50    0    34731  64032  0x0  0x13   ERSs        SU
1        1       0c:54:15:db:b7:4e 22   1      72.5M     58.5M 41   2:22:37    0    63498  57440  0x0  0x13   ERSs M      SU
1        1       88:44:77:4a:95:84 28   1      72.5M      6.0M 39   0:35:20    0    882    20336  0x0  0x13   ERSs S      SU
1        1       e0:76:d0:46:85:b6 4    1      65.0M     26.0M 35   0:31:56    0    34917  23424  0x0  0x13   ERSs        SU
2        1       a0:57:e3:3b:4c:51 3    157   325.0M    234.0M 24   5:51:21    60   26349  47056  0x0  0x13   ERs  WS     SU
2        1       2c:ff:ee:82:96:13 32   157   433.0M    325.0M 34   4:02:13    15   44924  44224  0x0  0x13   ER   WS     MU
2        1       20:0d:b0:33:44:52 50   157   234.0M     58.0M 47   2:52:25    15   4005   31792  0x0  0x13   ERs  WSM    MU
2        1       e0:dd:c0:3e:69:82 52   157   150.0M    150.0M 37   2:43:48    0    28329  56960  0x0  0x13   ER   WS     SU
//RADIO-ID:RADIO-ID
//WLAN-ID:WLAN-ID
//ADDR:终端MAC地址
//AID：标识ID
//CHAN：信道
//RATE_DOWN：发送速率
//RATE_UP：接受速率
//RSSI：接受信号强度指示
//ASSOC_TIME：在线时间
//IDLE：无流量时长（秒）
//TXSEQ：发送报文序列号
//RXSEQ：接收报文序列号
//ERP：是否为ERP保护用户
//STATE：认证关联状态，目前无参考意义，均为0x13
//CAPS：协议规定的终端能力值
```

#### 2.4 查看AP和AC的capwap隧道建立情况

```cpp
Ruijie#show capwap state
CAPWAP tunnel state, 1 peers, 1 is run:
Index     Peer IP              Port      State
1         3.3.33.3             5246      Run
```

#### 2.5 查看AP的版本及运行时间，来排查AP是否重启过

```cpp
Ruijie#show version
System description      : Ruijie Indoor AP720-L (802.11a/n/ac and 802.11b/g/n) By Ruijie Networks. //AP信息描述
System start time       : 2019-10-23 15:59:46 //AP启动时间
System uptime           : 42:00:44:31 //AP运行时间（天：时：分：秒）
System hardware version : 2.00 //AP硬件版本
System software version : AP_RGOS 11.1(9)B1P14, Release(06163010) //AP软件版本
System patch number     : NA //AP补丁序号
System serial number    : G1NT7LK327267 //AP序列号
System boot version     : 2.0.26 //AP boot版本
```

#### 2.6 查看该AP的BSSID及radio相关信息

```cpp
Ruijie#show dot11 wireless 1/0
Network Name (SSID): NULL //对应BBS标识
    Interface.................... Dot11radio 1/0 //接口名称
    Vlan (group) id.............. 0 //绑定的VLAN或者VLAN GROUP
    MAC Address.................. 0005.889f.3ddb //无线网卡的MAC地址
    Beacon Period................ 100 //Beacon帧发送周期
    RTS Threshold................ 2347 //要执行RTS/CTS握手的最小数据帧长度
    Fragment Threshold........... 2346 //分片阈值
    Radio Mode................... 11ng_ht20 //射频口模式
    Channel...................... 2412(1) //工作信道
    Noise Floor.................. -104 dBm //噪音
    Actual Tx Power.............. 13 dbm //实际发送功率
    Max Txpwr Limit.............. 16 dbm //最大发送功率
    Minimum Txpwr ............... 1 dbm //最小发送功率
    Channel width................ 20Mhz //带宽
    Current Tx Power Level....... 100% //当前功率百分比值
    Current CCA ................. 25 //CCA阈值
Tx/Rx Chain:
    Antenna Gain................. 3 //天线增益
    Tx Chain Mask................ 0x3 //发送天线掩码
    Num of Antenna Tx............ 2 //发送天线数
    Rx Chain Mask................ 0x3 //接收天线掩码
    Num of Antenna Rx............ 2 //接收天线数
Power Save:
    DTIM Period.................. 1 //DTIM周期
    DTIM Count................... 0 //DTIM个数
    Stations In Power Save....... 0 //节电STA个数
    Stations Total............... 5 //STA个数
11n Aggregation: 
    A-mpdu Status................ Enable //A-MPDU聚合状态
Tx Retries:
    Tx short    retries.......... 7 //短帧重传次数
    Tx long     retries.......... 4 //长帧重传次数
Total Stations:
    Total........................ 0 //当前射频口的STA总数
    Non-ERP...................... 0 //当前射频口的非 11G 下STA个数
    Non-HT....................... 0 //当前射频口的非 11N 下STA个数
    HT20......................... 0 //当前射频口的 11N 20M 频宽下STA个数
```

### 3. AC常见参数调整命令

#### 3.1 如何修改AP名称

```cpp
AP与WS无线控制器关联后，默认的名称为AP机身背面所贴标签上的MAC地址。
若需要修改AP的名称，则进行如下操作：
Ruijie(config)#ap-configaaaa.aaaa.aaaa
Ruijie(config-ap)#ap-name ap-name
```

#### 3.2 如何删除已经下线的AP名称

```cpp
//进行如下操作：
Ruijie(config)#noap-config ap-name //删除单个
Ruijie(config)#noap-config all //删除所有不在线的ap-config
//只有已经下线的AP的配置才能被删除。
```

#### 3.3 如何配置瘦AP的位置信息

```cpp
//参考配置如下：
Ruijie(config)#ap-config 001a.a9bf.ffdc
Ruijie(config-ap)#location 会议室
```

#### 3.4 如何修改AC建立capwap隧道使用的地址

```cpp
//需要升级到1B19及1B19以上版本
Ruijie(config)#ac-controller
Ruijie(config-ac)#capwapctrl-ip 2.2.2.2
```

#### 3.5 在瘦AP模式下静态配置AP的IP地址

```cpp
//参考命令：（修改该参数会导致AP重新建立隧道）
1.通过console或telnet登入到AP，进入全局模式（enable密码是apdebug）给AP配置静态IP地址、默认路由、ACIP地址 ：
Ruijie(config)#acipipv4 1.1.1.1 //配置AC IP地址
Ruijie(config)#apip172.16.1.34 255.255.255.0 172.16.1.109

2.AP和AC建立隧道之后，登入到AC给AP配置静态IP地址：
Ruijie(config)#ap-config220e     
Ruijie(config-ap)#acipipv4 1.1.1.1 //配置AC IP地址
Ruijie(config-ap)#ipaddress 172.16.1.34 255.255.255.0 172.16.1.109 //AP的地址、掩码和网关，配置后AP会重新建立隧道

//保存配置后重启AP这两个配置都不会消失。
```

#### 3.6 瘦AP如何切换工作频段

```cpp
//参考命令：
Ruijie(config)#ap-config 001a.a9bf.ffdc
Ruijie(config-ap)#radio-type 2 802.11b
//注：目前只有AP220-E 1.x、AP220-SE1.x、AP620-H 1.x 、AP220-E(M)-V2、AP120-W、AP3220-P、AP530-I v1.5x、AP740-I第三射频卡 支持射频卡工作频段的切换，其他AP射频卡工作频段均是固定，无法修改。
```

#### 3.7 如何关闭802.11n功能

```cpp
Ruijie(config)# ap-config  AP0001
Ruijie(config-ap)#no 11ngsupport enableradio 1 //关闭radio 1在2.4G下支持802.11n功能
Ruijie(config-ap)#no 11nasupport enableradio 2 //关闭radio 2在5G下支持802.11n功能
```

#### 3.8 如何关闭802.11b功能

```cpp
10.4(1b19)开始支持：
Ruijie(config)# ap-config  AP0001
Ruijie(config-ap)#no 11bsupport enableradio 1 //关闭radio 1在2.4G下支持802.11n功能
```

#### 3.9 瘦模式如何禁用AP的某个radio

```cpp
Ruijie(config)#ap-config ap-name //进入对应AP
Ruijie(config-ap)#no enable-radio 1 //禁用radio 1
```

#### 3.10 推荐将11b/g 1M、2M、5M，11a6M、9M 等低速率集进行关闭，避免个别用户发送过多低速报文影响整体无线性能。

```cpp
Ruijie(config)#ac-controller
Ruijie(config-ac)#802.11b network  rate 1 disabled
Ruijie(config-ac)#802.11b network  rate 2 disabled
Ruijie(config-ac)#802.11b network  rate 5 disabled
Ruijie(config-ac)#802.11g network  rate 1 disabled
Ruijie(config-ac)#802.11g network  rate 2 disabled
Ruijie(config-ac)#802.11g network  rate 5 disabled
Ruijie(config-ac)#802.11a network  rate 6 disabled
Ruijie(config-ac)#802.11a network  rate 9 disabled
```

#### 3.11 配置AC的设备时间同步给AP

```cpp
Ruijie(config)# ap-config  AP0001 //进入指定AP的配置模式
Ruijie(config-ap)#timestamp //配置AP0001 同步本AC的时间
```

### 4. AC&AP管理维护命令

#### 4.1 如何查看AP或AC web服务是否有打开，以及使用哪些端口

```cpp
Ruijie#show web-service / status //EG不用加status
webservice  :
  http      : enable //enable"启用"，disable"关闭"
            : port(80) //访问端口
  https     : enable //enable"启用"，disable"关闭"
            : port(4430) //访问端口
  guest-auth: disable //访客身份验证
//从上可知，默认AC的80端口和443端口均可以登入AC的web界面，即http和https均可以登入
```

#### 4.2 如何修改AP或AC web登入的端口

```cpp
Ruijie(config)#ip http port 8080 //(11.x)设备web登入的端口号从80更改为8080
Ruijie(config)#http port 8080 //(10.x)设备web登入的端口号从80更改为8080
```

#### 4.3 如何修改AC或者AP的web登入密码

```cpp
Ruijie(config)#webmaster level 0 username "admin" password "admin" //设置用户名密码都为admin
```

#### 4.4 AC上如何关闭瘦AP的web管理功能

```cpp
Ruijie(config)#ap-config "xxx" //xxx可以为ap的名称/MAC地址，则是对单个AP生效，xxx可以是all，则是对全部AP生效
Ruijie(config-ap)#exec-cmd mode config cmd "no enable service web-server"
```

#### 4.5 AC上如何关闭瘦AP的telnet功能

```cpp
Ruijie(config)#ap-config "xxx" //xxx可以为ap的名称/MAC地址，则是对单个AP生效，xxx可以是all，则是对全部AP生效
Ruijie(config-ap)#exec-cmd mode config cmd "no enable service telnet-server"
```

#### 4.6 AC上如何修改瘦AP web登入密码

```cpp
1.先建立一个ap-webmaster.txt的记事本，内容如下：
Ruijie(config)#webmaster level 0 username admin password "actest" //web登入的密码修改为actest
2.把这个ap-webmaster.txt文件上传到AC的flash上：
3.在AC上执行
Ruijie(config)#ap-config xxx
Ruijie(config-ap)#auto-cfg file flash:ap-webmaster.txt force
//xxx只能是all，对全部AP生效，或者在ap-group组底下配置，对组底下的Ap生效
```

#### 4.7 AC上如何修改瘦AP telnet使用用户名和密码登入

```cpp
Ruijie(config)#ap-config xxx
Ruijie(config-ap)#credential admin ruijie //telnet使用用户名admin密码ruijie登入
//xxx可以为ap的名称/MAC地址，则是对单个AP生效，xxx可以是all，则是对全部AP生效，也可以在ap-group组底下配置，对组底下的AP生效，
配置优先级："ap-config ap-name > ap-group > ap-config all"
```

#### 4.8 AP如何恢复出厂设置

```cpp
Ruijie#clear ap flash //10.x版本（1b19p2 17x开始支持） 
Ruijie(config)#apm factory-reset //11.x版本 
//AP110W/120W/130系列等WALL-AP有reset按键的可以长按设备的reset按钮3秒以上实现恢复出厂配置。
```

#### 4.9 AC如何恢复出厂设置

```cpp
//删除配置文件config.text
Ruijie#del config.text
Are you sure you want to delete "config.text"?[Yes/No]y //键入“y”
//查看配置文件config.text是否删除成功。如果不成功，重复步骤
Ruijie#dir
//重启设备
Ruijie#reload
Proceed with reload? [no]y //键入“y”
//操作完毕
```

### 5. AC&AP踢用户下线命令

#### 5.1 如何踢在线AP下线

```cpp
Ruijie(config)#ac-controller
Ruijie(config-ac)#kick-ap ?
  all    Kick all ap Debug. //所有AP
  H.H.H  MAC address //单个AP的mac地址
Ruijie(config-ac)#kick-ap aaaa.aaaa.aaaa
```

#### 5.2 如何踢在线用户下线

```cpp
Ruijie(config)#ac-controller
Ruijie(config-ac)#client-kick ?
  H.H.H  MAC address //单个用户的mac地址
Ruijie(config-ac)#client-kick aaaa.aaaa.aaaa
//但是踢用户下线后，用户可能会重新连接上来，建议可以加黑名单后再踢用户下线
```

#### 5.3 如何踢web认证用户下线

```cpp
Ruijie#clear web-auth user ?
  all   Process all users //所有用户
  ip    User ip address //基于认证用户的ip
  mac   User MAC //基于认证用户的mac
  name  User name //基于认证用户的用户名
Ruijie#clear web-auth user mac aaaa.aaaa.aaaa
```

#### 5.4 如何踢802.1x认证用户下线

```cpp
Ruijie#clear dot1x user ?
  all   All user //所有用户
  ip    Clear user by ip //基于认证用户的ip
  mac   Clear user by mac //基于认证用户的mac
  name  Clear user by name //基于认证用户的用户名
Ruijie#clear dot1x user aaaa.aaaa.aaaa
```

#### 5.5 如何在AC上重启AP

```cpp
Ruijie(config)#ac-controller
Ruijie(config-ac)#reset ?
  all     Reset the all APs in this AC //所有AP
  single  Reset the single ap //单个AP
Ruijie(config-ac)#reset single aaaa.aaaa.aaaa //AP名字
```

#### 5.6 如何在AC上给AP恢复出厂设置

```cpp
Ruijie(config)#ac-controller
Ruijie(config-ac)#factory-reset ?
  WORD  Set the name //AP名字
Ruijie(config-ac)#factory-reset AP1
```

#### 5.7 胖模式下如何踢用户下线

```cpp
Ruijie(config)#wids
Ruijie(config-wids)#kickout client ?
  H.H.H  MAC address //用户mac地址
Ruijie(config-wids)#kickout client aaaa.aaaa.aaaa
//但是踢用户下线后，用户可能会重新连接上来，建议可以加黑名单后再踢用户下线
```

### 6. 无线AC11.X版本升级常见维护命令

#### 6.1 无线AC如何限制每次提示升级的AP个数？

```cpp
//AC全局模式下：
Ruijie(config)#ac-controller  
Ruijie(config-ac)#capwap upgrade max-concurrent 10  //限制为 10，默认限制15个
```

#### 6.2 如何查看AC中有哪些AP的型号和版本（10.x、11.x均支持，前提需开启wlan diag，用于版本升级时查看是否需要升级）

```cpp
Ruijie#show wlan diag network
```

#### 6.3 如何在AC上对单台AP进行升级？

```cpp
先把ap 的软件版本传到AC的flash中，然后在AC上进行以下操作。（只对已和AC建立隧道的AP起作用）
Ruijie(config-ac)#active-bin-file ap1.bin //激活AP软件版本，“ap1.bin”表示ap的版本在AC的flash中保存名称是 ap1.bin 
Ruijie(config-ac)#ap-serial 320 AP320-I hw-ver 1.x //定义AP的产品系列,名称是320，产品是硬件版本是1.x的AP320-I
Ruijie(config-ac)#exit Ruijie(config)#ap-config 1414.0123.2345 //进入要升级的AP320-I的ap-config 
Ruijie(config-ap-config)#ap-image ap1.bin //下发软件版本，版本下发成功后AP会自动重启
```

#### 6.4 如何查看AC历史升级记录？

```cpp
Ruijie#show upgrade history //在11.x版本通过show upgrade history 命令可查看具体什么时间点，通过哪种方式，升级的文件等
```

### 7. 本地转发常见维护命令

#### 7.1 如何在AC上确认无线是本地转发？

```cpp
10.x或者11.x版本
wlan-config 1 WDDSNNY
 ssid-code utf-8
 band-select enable
 tunnel local //tunnel local为本地转发 
Ruijie#show wlan-config cb 1
WLAN ID.................................. 1
SSID..................................... WDDSNNY
Profile..................................
MAC Mode................................. Local
Tunnel Mode.............................. Local Bridging //Local Bridging为本地转发
Suppress SSID............................ Disable
Sta-limit................................ 0
NAS ID...................................
Band Select.............................. Enable
SSID Code................................ utf-8
```

#### 7.2 如何在ap上确认无线是否为本地转发？

```cpp
"10.x版本"
Ruijie#show run interface dot11radio 1/0.1
//mac-mode locall 为本地转发

"11.x版本"
Ruijie#debug fwd dump-mode
wlan 1 tunnel local //local为本地转发
```

### 8. 黑白名单常见维护命令

#### 8.1 如何查看配置的基于ssid和全局的黑白名单列表？

```cpp
基于全局:
Ruijie#show wids whitelist //查看白名单
Ruijie#show wids blacklist static //查看黑名单

基于ssid：
Ruijie#show wids ssid-filter whitelist all //查看基于ruijie ssid的白名单
Ruijie#show wids ssid-filter blacklist all //查看所有基于ssid的黑名单
Ruijie#show wids ssid-filter whitelist in-ssid test //查看基于test ssid的白名单
Ruijie#show wids ssid-filter blacklist in-ssid test //查看基于test ssid的黑名单
```

#### 8.2 命令行下如何全部删除黑白名单中的终端mac？

```cpp
Ruijie(config)#wids
Ruijie(config-wids)#reset whitelist all //删除全局白名单下的终端mac
Ruijie(config-wids)#reset static-blacklist all //删除全局黑名单下的终端mac
Ruijie(config-wids)#reset ssid-filter ssid all //删除基于所有ssid黑白名单下的终端mac
Ruijie(config-wids)#reset ssid-filter in-ssid ruijie //删除基于ruijie ssid黑白名单下的终端mac
```

### 9. 漫游常见维护命令

#### 9.1 查看某个特定用户是否漫游？

```cpp
Ruijie#show ac-config client detail aaaa.aaaa.aaaa
Mac Address         :aaaa.aaaa.aaaa
IP Address          :192.168.0.100
Wlan Id             :1
Vlan Id             :1
Roam State          :Local //Local：非漫游，Roam：漫游
Association ID      :1
Associated Ap Information:
AP Name             :AP名称
AP IP               :192.168.0.120
```

#### 9.2 如何查看所有漫游用户？

```cpp
Ruijie#show mobility user
========= show mobility user =========
Mobility user number: 0

STA-MAC         IPv4-Address IPv6-Address    WLAN  TYPE             ROC-VLAN  RIC-VLAN
--------------- ------------ ------------    ----  ----             ----------  --------
aaaa.bbbb.aaaa  10.0.0.1                     1     LC(AC内漫游用户)   2           2
aaaa.aaaa.aaaa  10.0.0.1                     2     RIC(AC间漫入用户)  2           2
aaaa.aaaa.cccc  10.0.0.1                     3     ROC(AC间漫出用户)  2           2
```

#### 9.3 查看跨AC漫游信息

```cpp
Ruijie#show mobility status  mgroup_name
```

#### 9.4 如何查看AC上MAC为xxx的终端漫游轨迹信息？

```cpp
Ruijie#show mobility user roam-track aaaa.aaaa.aaaa
ID  AC-Info   AP-Info            Online-time(d:h:m:s)
--  -------   ----------------   --------------------
1   HOME AC   aaaa.aaaa.aaaa/2   0:00:10:50
2   HOME AC   aaaa.aaaa.aaaa/2   0:20:40:43
3   HOME AC   aaaa.aaaa.aaaa/2   6:00:10:32

//ID:漫游顺序的编号
//AC-Info:所属AC的信息
//AP-Info:所属AP的信息
//Online-time(d:h:m:s):关联的时长
```

### 10. WEB认证常见维护命令

#### 10.1 清除通过web认证的用户

```cpp
通过如下命令可以清掉用户：
Ruijie#clear web-auth user H.H.H //H.H.H 为无线用户mac地址
```

#### 10.2 查看web认证的用户相关信息

```cpp
Ruijie#show web-auth user all
Ruijie#show web-auth user ip 192.168.0.11
```

#### 10.3 显示WEB认证相关控制信息

```cpp
Ruijie#showeb-auth control
```

#### 10.4 显示HTTP 重定向的配置

```cpp
Ruijie#show http redirect
```

