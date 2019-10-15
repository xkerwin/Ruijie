# 4.3 删除配置文件

删除配置文件就是把NVRAM中的 startup-config 删除。

## 模式：

特权配置模式。

## 命令：

`Ruijie#delete flash:config.text`

## 说明：

config.text是配置文件在NVRAM中的文件名，它被删除后，再重启设备时会自动进入 setup 配置模式。

## 注：

有些设备没有setup配置模式，它在没有配置文件时会自动按照缺省值启动。

