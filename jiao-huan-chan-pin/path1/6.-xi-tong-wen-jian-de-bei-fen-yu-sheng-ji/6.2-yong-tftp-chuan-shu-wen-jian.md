# 6.2 用TFTP传输文件

## 准备工作：

1. 设备已经配置了IP地址，且可以与计算机正常通信（可以用ping命令检查）。
2. 在计算机上运行TFTP服务器软件，并设置好文件保存的路径。如下图：

## 把设备中的文件传输到计算机中：

用控制台或Telnet登录设备，然后在特权模式下执行以下命令：

`Ruijie#copy filename tftp`

filename是交换机或路由器上的文件。例如：

## ①把running-config传输到计算机中

```java
Ruijie#copy running-config tftp
Address or name of remote host [ ]?192.168.1.2
Destination filename [ ]?S1-config.txt
```

192.168.1.2是目的计算机的IP地址，应根据实际情况设置。S1-config.txt是在计算机上保存的文件名，可自行命名。

以上操作也可以直接写作：

`Ruijie#copy running-config tftp://192.168.1.2/S1-config.txt`

## ②把主体文件传输到计算机中

```java
Ruijie#copy flash:cs3550b.bin tftp
Address or name of remote host [ ]?192.168.1.2
Destination filename [ ]?cs3550b.bin
```

主体文件的扩展名一般是 bin，不同型号的设备文件名有所不同，应先用 dir 命令查看后再备份。

以上操作也可以直接写作：

`Ruijie#copy flash:cs3550b.bin tftp://192.168.1.2/cs3550b.bin`

## 注意：

由于在设备中，主体文件有固定的名字，为了方便以后的回传，最好使用相同的名字备份，且要做好记录。

其它文件的传输方法和以上实例类似。

把计算机中的文件回传到设备中：

## ①把计算机中备份的配置文件回传到设备中

```java
Ruijie#copy tftp running-config
Address or name of remote host [ ]?192.168.1.2
Source filename [ ]?S1-config.txt
```

本例把计算机中的 S1-config.txt 文件回传到设备中，使它成为 running-config。

## ②把计算机中备份的主体文件回传到设备中

```java
Ruijie#copy tftp flash:cs3550b.bin
Address or name of remote host [ ]?192.168.1.2
Source filename [ ]?cs3550b.bin
```

## 注意：

各个设备的主体文件有固定的文件名和版本，回传时一定要保证版本正确，文件名正确，不然会导致设备复位后不能启动。

## ③把计算机中打包的主体文件回传到设备中

有些型号的设备主体文件的扩展名为 udp，该文件实际上是一个软件包，里面包含了 bin 文件和Web配置软件。

udp 文件不能用 copy tftp flash 命令传输，应该使用 copy tftp update 命令传输。

```java
Ruijie#copy tftp update
Address or name of remote host [ ]?192.168.1.2
Source filename [ ]?rgnos.upd
```

