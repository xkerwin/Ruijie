# 6.1 2层Access Port（普通口）的配置

3层交换机的所有物理接口默认都是2层Access Port，所以不需要进行配置。

Access接口具有以下特性：

1. Access接口是2层口，不能为它配置IP地址，没有路由功能。
2. 每个Access接口只能属于一个VLAN（默认是VLAN1），它只能转发属于同一个VLAN的帧。

