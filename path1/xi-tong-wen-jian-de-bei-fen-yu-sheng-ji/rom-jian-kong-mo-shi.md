# 6.4 ROM监控模式

## 进入ROM监控模式有两种方法：

1. 如果设备在启动时，无法在Flash中找到设备的主体文件，便直接进入ROM监控模式。
2. 用手工进入，先用Console线连接设备和计算机，并在计算机上运行终端仿真软件（如：超级终端），然后开启设备，在开机后的3秒内按下 Ctrl+C，便进入ROM监控模式了。

进入监控模式后，先显示一些版本信息，然后是主菜单：\(\)中为注解

```java
Main Menu:

  1. TFTP Download & Run (用TFTP传入文件并运行)

  2. TFTP Download & Write Into File (用TFTP传入文件并写入Flash)

  3. X-Modem Download & Run (用Xmodem传入文件并运行)

  4. X-Modem Download & Write Into File (用Xmodem传入文件并写入Flash)

  5. List Active Files (列出Flash中文件信息)

  6. List Deleted Files (列出Flash中删除文件的信息)

  7. Run A File (运行一个文件)

  8. Delete A File (删除一个文件)

  9. Rename A File (重命名一个文件)

  a. Squeeze File System (碎片整理)

  b. Format File System (格式化Flash)

  c. Other Utilities (其它)

  d. hardware test

  e. TFTP Download & Update (用TFTP传入打包的主体文件)

  f. X-Modem Download & Update (用Xmodem传入打包的主体文件)

Please select an item:
```

选项1和选项2的区别在于：选项1把文件传入到内存中，不写入Flash，所以在重启设备后，仍会使用原来的文件；选项2是把文件传入内存并写入Flash，使它永久有效。

通常，如果我们想要传入一个文件进行测试，应该使用选项1，如果想要传入一个永久有效的文件，应该使用选项2。

## 实例：

假设某路由器的主体文件被损坏，现把TFTP服务器上备份的文件传入路由器的Flash中，使路由器恢复正常。

启动路由器，由于主体文件损坏，进入ROM监控模式，选择项目2进行传输。

```java
Please select an item: 2
File name[]: 85_1_b10_r36.bin
Local IP[]: 192.168.1.1
Remote IP[]: 192.168.1.2
```

`85_1_b10_r36.bin`是主体文件名，`Local IP`是路由器IP地址，`Remote IP`是TFTP服务器的IP地址，这两个地址必须在同一网络中。然后就开始传输了。其中TFTP服务器可按前面的方法设置。 传输完成后，重新开启路由器，就可以使用新的主体文件了。

