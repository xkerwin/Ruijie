# 4.4 备份配置文件

通常我们把配置文件备份到TFTP服务器上，在需要时可以再从TFTP服务器上把配置文件回传到设备中。

## 准备：

在作为TFTP服务器的计算机上打开TFTP服务器软件，并设置存放文件的路径（如下图）。然后在交换机或路由器上进行以下操作。

## 模式：

特权配置模式。

## 命令：

```java
Ruijie#copy running-config tftp
Address or name of remote host [ ]?192.168.0.2
Destination filename [ ]?S1-config.txt
```

## 说明：

输入 copy 命令后还需要回答两个问题，一是TFTP服务器的地址，本例中假设为192.168.0.2，二是备份的配置文件名，本例中假设为S1-config.txt。备份成功后，在TFTP服务器指定的目录中可看到此文件。

## 从TFTP服务器回传配置文件：

```java
Ruijie#copy tftp running-config
Address or name of remote host [ ]?192.168.0.2
Source filename [ ]?S1-config.txt
```

## 说明：

有些设备不支持备份running-config文件，但支持备份startup-config文件。

