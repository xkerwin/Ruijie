# 1.1 配置主机名

## 配置主机名

## 模式：

全局配置模式。

## 命令：

`hostname name`

## 参数：

name是要设置的主机名，必须由可打印字符组成，长度不能超过255个字符。

主机名一般会显示在提示符前面，显示时最多只显示22个字符。

## 2、删除配置的主机名

在全局配置模式下，用 `no hostname` 命令可删除配置的主机名，恢复默认值。

## 配置举例：

配置交换机的名字为S3550-1。

```java
Switch>enable
Switch#configure terminal
Switch(config)#hostname S3550-1
S3550-1(config)#
```

