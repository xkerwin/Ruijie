# 5.3 系统保护信息的查看

## 模式：

特权模式。

## 1、查看系统保护信息：

```java
Switch#show system-guard interface interface-id
```

`interface interface-id`是可选的，用于查看指定接口的IP系统保护信息。如：

```java
Switch#show system-guard
```

`detect-maxnum number :` 100 监控主机的最大数目

`isolated host number :` 11 已隔离的主机数

```java
interface　state　　isolate time　same-attack-pkts　scan-attack-pkts

---------　-------　------------　----------------　----------------

Fa0/1　　　ENABLE　　120　　　　　　　20　　　　　　　10
Fa0/2　　　DISABLE　 110　　　　　　　21　　　　　　　11

......
```

## 2、查看被隔离的主机：

```java
Switch#show system-guard isolated-ip interface interface-id
```

`interface interface-id`是可选的，用于查看指定接口的被隔离主机。如：

```java
Switch#show system-guard isolated-ip
```

```java
interface　　ip-address　　　isolate reason　　remain-time(second)

---------　--------------　-----------------　--------------------

Fa0/1　　　192.168.5.119　　scan ip attack　　　　110
Fa0/1　　　192.168.5.131　　same ip attack　　　　62
```

各个栏目依次为：隔离IP出现的端口、隔离的IP地址、隔离原因、隔离的剩余时间。

一般交换机的硬件只支持每端口隔离100~120个IP地址，如果一些用户的isolate reason中显示“chip resource full”，表明这些用户实际上没有被隔离，管理员应采取其它措施来处理这些攻击者。

## 3、查看被监控的主机：

```java
Switch#show system-guard detect-ip interface interface-id
```

被监控的主机是指被怀疑正在进行攻击。`interface interface-id`是可选的，用于查看指定接口的被监控主机。如：

```java
Switch#show system-guard detect-ip
```

```java
interface　　ip-address　　same ip attack packets　scan ip attack packets

---------　--------------　----------------------　--------------------

Fa0/1　　　192.168.5.110　　　　　0　　　　　　　　　　　8
Fa0/1　　　192.168.5.121　　　　　12　　　　　　　　　　 2
```

