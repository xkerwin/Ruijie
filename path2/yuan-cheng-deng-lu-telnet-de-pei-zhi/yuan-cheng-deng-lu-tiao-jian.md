# 4.1 远程登录条件

一台交换机能够通过Telnet登录的条件是：

1. 交换机已经配置了IP地址；
2. 交换机已经配置了远程登录密码；
3. 交换机已经配置了特权密码；
4. 交换机已经接入网络并开始工作。

这时，我们可以通过网络中的一台计算机，在命令行下输入“telnet 交换机IP地址”登录到交换机上对交换机进行配置。

## 如果登录的交换机没有配置远程登录密码，会显示`Password required, but none set`的错误提示信息；如果没有设置特权密码，在进入特权模式时会显示`%No password set`的错误提示信息。

所以，对于一台新购置的交换机，必须先用控制台为交换机配置IP地址和远程登录密码，以后就可以用远程登录管理这台交换机了。

## 配置举例：

用控制台为交换机配置IP地址、远程登录密码和特权密码。

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface vlan 1
Switch(config-if)#ip address 192.168.1.5 255.255.255.0
Switch(config-if)#exit
Switch(config)#line vty 0 4
Switch(config-line)#login
Switch(config-line)#password 123
Switch(config-if)#no shudown
Switch(config-line)#exit
Switch(config)#enable secret 456
Switch(config)#end
Switch#
```

完成以上配置后，我们可以通过网络中的一台计算机，用 `telnet 192.168.1.5` 登录交换机，登录密码为123。登录后，**进入特权模式的密码为456。**

