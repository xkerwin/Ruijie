# 1.2 设置时区

锐捷交换机的缺省时区是东8区（北京时间）。

## 模式：

特权模式。

## 命令：

```java
Switch#clock time-zone time-zone
```

参数 `time-zone` 是设置的时区，取值范围为-23~23，如8表示东8区，-8表示西8区，0表示格林威治标准时间。

## 配置举例：

设置时区为东6区。

```java
Switch>enable
Switch#clock time-zone 6
```

