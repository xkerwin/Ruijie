# 3.1 交换机的初始化配置

新出厂的交换机没有配置文件，或者你删除了交换机的配置文件，在用控制台登录时，可以进行一些基础配置，你可以在此处配置一些基本参数。（注：有些设备没有setup配置模式，它在没有配置文件时会自动按照缺省值启动。） 把控制台连接到交换机上，打开超级终端，如果交换机中没有配置文件，就会进入setup配置模式：

```java
--- System Configuration Dialog ---
At any point you may enter a question mark '?' for help.
Use ctrl-c to abort configuration dialog at any prompt.
Default settings are in square brackets '[]'.
Continue with configuration dialog? [yes/no]: y
Enter IP address: 192.168.1.5
Enter IP netmask: 255.255.255.0
Enter host name [Switch]:
The enable secret is a one-way cryptographic secret use
instead of the enable password when it exists.
Enter enable secret: 123
Would you like to configure a Telnet password? [yes/no]: y
Enter Telnet password: 456
Would you like to disable web service? [yes/no]: y
The following configuration command script was created:

int VLAN 1
ip address 192.168.1.5 255.255.255.0
!
enable secret 5 $xH.Y*T7xC,tz[V/xD+S(\W&xG1X)sv'
!
end
Use this configuration? [yes/no]: y

Building configuration...
OK
```

在上面的配置中，依次配置了管理IP、子网掩码、交换机名、特权密码、远程登录密码等，并且关闭了Web服务。最后一步选择“yes”，则交换机把生成的配置文件应用于交换机。

