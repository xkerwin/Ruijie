# 5.3 目录操作

Flash中的文件可以使用树形的目录结构，文件可以存放在不同的子目录中，也可以在目录之间移动、复制文件。

所有目录操作都是在特权模式下进行。

## 1、创建目录：

`Ruijie#mkdir directory`

directory是要创建的目录名称。例如：

`Ruijie#mkdir txt`

表示在当前目录中创建一个名为 txt 的子目录。

## 2、切换目录：

`Ruijie#cd directory`

directory是要进入的目录名称。其中当前目录用“.”表示，上级目录用“..”表示，根目录用“/”表示。例如：

①进入 txt 目录：

`Ruijie#cd txt`

②返回上一级目录：

`Ruijie#cd ..`

③返回根目录：

`Ruijie#cd /`

注意：在 cd 后要有空格，用 cd/ 是错误的。

## 3、删除目录：

`Ruijieh#rmdir directory`

directory是要删除的目录名称。

注意：本命令只能删除空目录。例如：

`Ruijie#rmdir txt`

## 4、查看目录下的文件：

`Ruijie#ls pathname`

pathname是路径名，如果省略路径，则显示当前目录下的文件。例如：

`Ruijie#ls`

显示当前目录下的文件列表。

## 5、复制文件：

把文件从一个目录复制到另一个目录中。

`Ruijieh#cp sour pathname dest pathname`

sour pathname是源文件，dest pathname是目的文件。例如：

`Ruijie#cp sour c1.txt dest ./txt/c1.txt`

表示把当前目录中的 c1.txt 复制到 txt 子目录中。

注意：cp 命令不支持通配符，也不支持目录的复制。

## 6、移动文件：

把文件从一个目录移动到另一个目录中。

`Ruijieh#mv sour pathname dest pathname`

sour pathname是源文件，dest pathname是目的文件。例如：

`Ruijie#mv sour c1.txt dest ./txt/c1.txt`

表示把当前目录中的 c1.txt 移动到 txt 子目录中。

## 7、删除文件：

`Ruijieh#rm filename`

filename是要删除的文件名。例如：

`Ruijie#rm c1.txt`

表示删除当前目录中的 c1.txt 文件。

