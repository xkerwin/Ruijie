# 1. 实例----用3层交换机划分子网

3层交换机S3550把局域网分割成两个子网：

## 子网1：

10.1.1.0/24，连接在FastEthernet0/1接口，网关地址为10.1.1.1/24。

## 子网2：

10.2.2.0/24，连接在FastEthernet0/2接口，网关地址为10.2.2.1/24。

## 配置S3550：

```java
Switch>enable
Switch#configure terminal

#配置交换机名字
Switch(config)#hostname S3550

#配置F0/1为3层路由口
S3550(config)#interface f0/1
S3550(config-if)#no switchport
S3550(config-if)#ip address 10.1.1.1 255.255.255.0

#配置F0/2为3层路由口
S3550(config-if)#interface f0/2
S3550(config-if)#no switchport
S3550(config-if)#ip address 10.2.2.1 255.255.255.0
S3550(config-if)#exit

#启用IP路由
S3550(config)#ip routing
S3550(config)#end

#查看配置结果
S3550#show running-config

#保存配置
S3550#copy running-config startup-config
```

## 说明：

`no switchport` 命令用于把2层口转换为3层路由口。只有3层口才能配置IP地址，2层口不能配置。

`ip routing` 命令用于启用IP路由。如果不启用IP路由功能，两个子网间将不能通信。（有些种类交换机的IP路由默认是启用的，此时可以没有此命令）。

在本网络中，两个2层交换机S1和S2不需要进行配置。

配置计算机时，PC1和PC2的默认网关应该设置为10.1.1.1，PC3和PC4的默认网关应该设置为10.2.2.1。

## 效果验证：

PC1和PC2属于同一个子网，彼此间可以通信，也能通过“网上邻居”共享文件。PC3和PC4也是如此。

两个子网间也可以通信，但不能通过“网上邻居”共享彼此的文件。

