# 2.3 配置特权口令

特权口令是从用户模式进入特权模式时设置的口令。

## 1、设置特权口令

## 模式：

全局配置模式。

## 配置命令：

```java
Ruijie(config)#enable password password
Ruijie(config)#enable secret password
```

`enable password password` 命令配置的口令在配置文件中是用简单加密方式存放的。（有些种类的设备是用明文存放的）

`enable secret password` 命令配置的口令在配置文件中是用安全加密方式存放的。

## 说明：

以上两种口令只需要配置一种，如果两种都配置了，则两个口令不应该相同，且用secret定义的口令优先。

## 2、删除配置的特权口令：

```java
Ruijie(config)#no enable password
Ruijie(config)#no enable secret
```

## 配置举例：

```java
Ruijie>enable
Ruijie#configure terminal
Ruijie(config)#enable secret 123
```

本例设置特权口令为123。使用安全加密的密文存放。

## 说明：

本部分配置的特权口令是为最高的15级设置的口令，如果想要使用多级别的特权模式，需要先用 privilege 命令为相应级别授权，再用 enable secret 命令配置该级别的口令。

