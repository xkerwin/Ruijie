# 7. 密码丢失的解决方法

如果忘记了路由器或交换机的登录密码，可以用以下方法解决：

用一台计算机作为控制台，用Console线连接在设备上，在计算机上运行终端仿真程序（如：超级终端）。

## ① 重启设备，在超级终端上按下 Ctrl+C，使设备进入ROM监控模式。

```java
Main Menu:

  1. TFTP Download & Run

  2. TFTP Download & Write Into File

  3. X-Modem Download & Run

  4. X-Modem Download & Write Into File

  5. List Active Files

  6. List Deleted Files

  7. Run A File

  8. Delete A File

  9. Rename A File

  a. SqueezeFile System

  b. Format File System

  c. Other Utilities

  d. hardware test

  e. TFTP Download & Update

  f. X-Modem Download & Update

Please select an item: 5
```

使用项目5，列出Flash中的文件目录，找到其中的配置文件（通常是名为config.text的文件）。

## ② 用项目9更改配置文件的文件名。

```java
Please select an item: 9
Old file name input.
Enter File Name (Input ESC to quit: config.text
New file name input.
Enter File Name (Input ESC to quit: config.bak
```

## ③ 重启设备，由于找不到配置文件，设备以默认参数启动，此时原有的配置也没有了。

## ④ 进入特权模式，把原来的配置文件再装入设备。

```java
Ruijie>enable
Ruijie#copy flash:config.bak running-config
Ruijie#
```

这样就恢复了原来的配置。由于此时已经进入特权模式，可以用命令删除原来的密码，也可以重新配置新密码。

## ⑤ 各部分密码都重新配置后，保存配置文件，以后就可以用新密码登录了。

```java
Ruijie#copy running-config startup-config
```

