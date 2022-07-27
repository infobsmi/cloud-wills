# CloudShell

腾讯云计算 为每位用户提供了免费的CloudShell服务。并且提供了免费的1GB存储，挂载目录位于 
/home/cloudshell/data

你可以把文件放到这个目录下面

腾讯会给你保存 120天，你可以随时访问这个cloudshell功能，自动续期120天

## 配置ssh 脚本，让你快速利用cloudshell 访问管理服务器

现在介绍给大家，如何配置 ssh脚本，把cloudshell 做为一个堡垒机工具，让你管理你的服务器。

首先我们创建一个脚本，名字为 pssh, 放到/home/cloudshell/data/pssh

内容如下


```bash
#!/bin/sh
set -ex
export SSHCLI="ssh -v -p 3809 -i ./id_rsa -o StrictHostKeyChecking=no"
case $@ in

webserver)
$SSHCLI root@webserver.baidu.host.com
;;

help)
echo "you can type like webserver"
;;

*)
echo "type help to see help"
;;


esac
```

上面的实例，我们有一台webserver.baidu.host.com的机器，它的ssh端口为3809， 我们写的这个bash脚本，定义了几个参数，当你输入的参数是缩写webserver的时候，就会连接到这个host的ssh

比如你执行

```bash
./pssh webserver

```

到这里，你就连上了。

如果你需要加更多的主机，你只需要更新上面的代码，复制多一份webserver) 就行了

记得改成其他名字，不能出现冲突。

