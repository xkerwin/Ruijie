# 2.1 命令模式的切换

交换机和路由器的模式大体可分为四层：用户模式→特权模式→全局配置模式→其它配置模式。 进入某模式时，需要逐层进入。

| 要求 | 命令举例 | 说明 |
| :--- | :--- | :--- |
| 进入用户模式 |  | 登录后就进入 |
| 进入特权模式 | `Ruijie>enable`  **Ruijie\#** | 在用户模式中输入enable命令 |
| 进入全局配置模式 | `Ruijie#configure terminal`  **Ruijie\(config\)\#** | 在特权模式中输入conf t命令 |
| 进入接口配置模式 | `Ruijie(config)#int f0/1`  **Ruijie\(config-if\)\#** | 在全局配置模式中输入int命令，该命令可带不同参数 |
| 进入线路配置模式 | `Ruijie(config)#line console 0`  **Ruijie\(config-line\)\#** | 在全局配置模式中输入line命令，该命令可带不同参数 |
| 进入路由配置模式 | `Ruijie(config)#router rip`  **Ruijie\(config-router\)\#** | 在全局配置模式中输入router命令，该命令可带不同参数 |
| 进入VLAN配置模式 | `Ruijie(config)#vlan 3`  **Ruijie\(config-vlan\)\#** | 在全局配置模式中输入vlan命令，该命令可带不同参数 |
| 退回到上一层模式 | `Ruijie(config-if)#exit`  **Ruijie\(config\)\#** | 用exit命令可退回到上一层模式 |
| 退回到特权模式 | `Ruijie(config-if)#end`  **Ruijie\#** | 用end命令或Ctrl+Z可从各种配置模式中直接退回到特权模式 |
| 退回到用户模式 | `Ruijie#disable`  **Ruijie&gt;** | 从特权模式退回到用户模式 |

说明：int等命令都是带参数的命令，应根据情况使用不同参数。 特例：当在特权模式下输入 Exit 命令时，会直接退出登录，不是回到用户模式。从特权模式返回用户模式的命令是 disable。

