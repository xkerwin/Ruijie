# 5.2 文件操作

所有文件操作都是在特权模式下进行。

## 1、查看Flash中文件目录：

```java
Ruijie#dir
Ruijie#dir
Directory of flash:/
<DIR>　　　　　　　Dec 11 2002　09:41:34　　temp
-rw-　　　　511　 Dec 11 2002　10:11:08　　conf_bak.text
-rw-　　　 1002　 Jan 15 2003　09:20:19　　config.text
-rw-　　2833568　　Jan 14 2003　19:21:37　　cs3550b.bin
-rw-　　　　 80　　Jan 14 2002　08:50:24　　vlan.dat
```

列表中列出的是处于激活状态的文件信息。

`Ruijie#dir delete`

该命令用于查看处于删除状态的文件信息。

## 2、删除文件：

`Ruijie#delete flash:filename`

filename是删除的文件名。例如：

`Ruijie#delete flash:conf_bak.text`

删除的文件名被标记为删除状态，用 dir delete 命令可以看到。

## 3、查看文件内容：

`Ruijie#more flash:filename`

filename是文件名。例如：

`Ruijie#more flash:config.text`

本命令只能查看文本文件。

## 4、重命名文件：

`Ruijieh#rename flash:filename flash:newname`

filename是原文件名，newname是新文件名。例如：

`Ruijie#rename flash:config.text flash:config.old`

对主体文件的重命名要谨慎，它会导致设备复位后不能启动。

## 5、碎片整理：

`Ruijieh#squeeze flash:`

碎片整理可以把处于删除状态的文件彻底清除，腾出空间保存新文件。

## 6、格式化：

`Ruijieh#format flash:`

格式化会清除Flash中所有文件，它会导致设备复位后不能启动，要慎重使用。

