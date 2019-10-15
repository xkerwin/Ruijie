# 4.5 查看Telnet Server的状态

在特权模式下，用 `show service` 命令可以查看Telnet Server是否已被禁用。

## 举例：

查看交换机Telnet Server的状态。

```java
Switch>enable
Switch#show service
SSH-server : Enabled
Snmp-agent : Disabled
Telnet-server : Enabled
Web-server : Enabled
```

`show service`命令显示了SSH Server、SNMP Agent、Telnet Server和Web Server四种管理方式的使能状态，`Enabled`为开启，`Disabled`为关闭。

