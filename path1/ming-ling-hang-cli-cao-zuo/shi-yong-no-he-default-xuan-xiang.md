# 2.4 使用no和default选项

很多命令都有`no`选项和`default`选项。

`no` 选项可用来禁止某个功能，或者删除某项配置。 `default` 选项用来将设置恢复为缺省值。

由于大多数命令的缺省值是禁止此项功能，这时`default`选项的作用和 no 选项是相同的。但部分命令的缺省值是允许，这时`default`选项的作用和 no 选项的作用是相反的。

`no`选项和`default`选项的用法是在命令前加`no`或`defaule`前缀。如：

```text
no shutdown
no IP address
default hostname
```

相比之下，我们多使用`no`选项来删除有问题的配置信息。

