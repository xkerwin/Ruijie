# 交换产品常用命令

### 1. 环路检查

```cpp
//查看下联设备
show lldp nei
​
//查看端口流量信息
show interface counters summary
​
//查看端口流量信息
show interface counters rate
​
//清除端口流量数据
clear counters
```

### 2. 查看配置信息

```cpp
//查看设备当前的配置
show running-config
​
//查看设备的软件版本信息
show version
​
//查看设备的日志
show log
​
//查看设备的三层接口ip和掩码
show ip interface brief
​
//查看f0/1接口的信息，包括mac地址，流量信息等等
show interface f0/1
​
//查看交换接口的信息,包括状态、vlan、双工、速度和使用介质
show interface status
​
//查看交换接口所属的vlan信息
show vlan
​
//查看设备当前的CPU使用情况
show cpu
​
//查看设备当前接口的实时流量
show interface count rate
​
//查看设备当前的MAC地址
show member
​
//查看设备当前的MAC地址表
show mac-address-table
​
//查看设备当前的ARP表
show arp
​
//查看CPU利用率
show cpu
​
//查看内存利用率
show memory
​
//查看电源
show power
​
//查看风扇
show fan
​
//查看温度
show temperature
​
//查看时间
show clock
​
//查看交换机FLASH空间大小
dir
​
//查看路由表
show ip route
​
//查看交换机的IP地址信息
show ip interface brief
​
//查看交换机的接口状态信息
show interfaces status
​
//查看交换机的接口报文信息
show int g0/1 counters
​
//查看邻居设备信息
show lldp nei detail
```

### 3. 特殊命令

```cpp
//使用mgmt口ping的方法
ping oob ip address
​
//路由追踪
traceroute ip address
​
//使用指定ip address ping
ping ip address source ip address
​
//SSH
ssh -l username ip address
​
//通过MGMT接口SSH
ssh oob -l username ip address
```

### 4.重置交换机配置

```cpp
ruijie#dir //查看交换机的配置文件

ruijie#delete config.text //删除交换机的配置文件
Do you want to delete [flash:/config.text]? [Y/N]:yes

ruijie#reload //重启交换机生效
Reload system?(Y/N)yes
```

