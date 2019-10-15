# 5.2 在三层交换机上配置系统保护

在缺省情况下，3层交换机上防扫描的系统保护功能是关闭的，配置时，需要打开该服务。

## 1、打开系统保护功能：

## 模式：

接口配置模式。

## 命令：

```java
Switch(config-if)#system-guard enable
```

这条命令用于打开指定接口的系统保护功能。

## 说明：

这条命令只能用于3层口。你可以使用 interface range 命令在一批接口上进行设置。

## 2、关闭系统保护功能：

## 模式：

接口配置模式。

## 命令：

```java
Switch(config-if)#no system-guard
```

## 3、配置系统保护参数：

## 模式：

接口配置模式。

## ①配置攻击阀值：

攻击阀值是判断是否发生扫描攻击的条件，当系统检测到连续的扫描次数超过设定的阀值时就认为发生了扫描攻击。

攻击阀值有两个：一是 `scan dest ip attack packets`，它用于判断是否发生对一批网段进行扫描的攻击，每个端口的默认值都是每秒10个；另一是 `same dest ip attack packets`，它用于判断是否发生不存在的IP发送报文的攻击，每个端口的默认值都是每秒20个。你可以用命令修改它们。

## 命令：

```java
Switch(config-if)#system-guard scan-dest-ip-attack-packets number
Switch(config-if)#system-guard same-dest-ip-attack-packets number
```

`scan dest ip attack packets` 的取值范围是0~1000，单位是每秒报文数，默认值为10。如果设置为0表示不对这种攻击进行监控。

`same dest ip attack packets` 的取值范围是0~2000，单位是每秒报文数，默认值为20。如果设置为0表示不对这种攻击进行监控。

## 说明：

如果把攻击阀值设置太小，会导致判断攻击的准确度变差，容易误隔离正常上网的主机。

## ②配置隔离时间：

当保护系统发现攻击时，会自动隔离发动攻击的IP地址，隔离一段时间该IP地址会自动恢复通信。

## 命令：

```java
Switch(config-if)#system-guard isolate-time time
```

隔离时间的取值范围是30~3600，单位是秒，默认值为120秒。

## 说明：

当用户被隔离时，会发一个LOG记录到日志系统，解除隔离时也会发一个LOG通知，管理员可以在日志中进行查询。

## ③配置监控主机的最大数目：

这个数目是同时被隔离的和监控的IP地址的最大数量。

## 命令：

```java
Switch(config-if)#system-guard detect-maxnum number
```

number的取值范围是1~500，默认值为100个。

## 说明：

一般来说，这个数目保持在“实际运行的主机数/20”左右即可，当发现实际隔离的主机数已接近最大数值时，应适当扩大此数值。但如果你把它改小，会引起当前隔离的主机数据清空。

## 4、手工解除隔离的主机：

被隔离的IP在隔离时间到后会自动解除隔离，你也可以用命令提前解除某些主机的隔离。

## 模式：

特权模式。

## 命令：

```java
Switch#clear system-guard interface interface-id ip-address ip-address
```

用 1clear system-guard1 命令可清除所有隔离的IP；

用 `clear system-guard interface interface-id`命令可清除指定接口下所有隔离的IP；

用 `clear system-guard interface interface-id ip-address ip-address`命令可清除指定接口下指定的IP。

## 配置举例：

```java
Switch>enable
Switch#configure terminal
Switch(config)#interface range f0/1-5
Switch(config-if)#system-guard enable
Switch(config-if)#system-guard scan-dest-ip-attack-packets 20
Switch(config-if)#system-guard same-dest-ip-attack-packets 30
Switch(config-if)#end
Switch#
```

本例假设f0/1~f0/5都已经配置为3层路由口，然后在它们上面启用系统保护功能。

