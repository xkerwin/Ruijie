# 常规交换机配置模板

```cpp
!配置交换机名称，开启telnet，帐号密码

configure

hostname XXX

username ruijie privilege 15 password ruijie123

enable password ruijie123

line vty 0 4

login local

end

!配置Vlan

configure

vlan A

name XXX

interface vlan A

ip address 

end

!开启防环路配置

configure

spanning-tree

rldp enable

errdisable recovery interval 300

end

!接口配置

configure

interface range gigabitEthernet 0/a-b

description [XXX]

switchport access vlan ID

spanning-tree bpduguard enable

spanning-tree portfast

rldp port loop-detect shutdown-port

spanning-tree bpduguard enable

end

!配置回指路由/网关

configure

ip route 0.0.0.0 0.0.0.0 x.x.x.x
/
ip default-network x.x.x.x
```

