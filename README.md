# GotoSSH

- [English Version](#english)
- [中文版](#chinese)

<a name="english"></a>

## Description

GotoSSH is committed to helping you improve work efficiency.

There are some pics, they will show you to what this shell can do.

Normal auto login:

![](https://i.loli.net/2019/03/29/5c9cf654b339b.gif)

Login the jump server first, and then jump to the online server：

![](https://i.loli.net/2019/03/29/5c9cf6c81ad1f.gif)

![](https://i.loli.net/2019/03/29/5c9cf6ee38d18.gif)

Login the server and view the log：

![](https://i.loli.net/2019/03/29/5c9cf72b7b707.gif)

Login the jump server and then login the online sever to view the log：

![](https://i.loli.net/2019/03/29/5c9cf76aad6ac.gif)

Copy file from the remote server：

![](https://i.loli.net/2019/03/29/5c9cf782c0db4.gif)

Copy file from the online server：

![](https://i.loli.net/2019/03/29/5c9cf7b506db0.gif)


## Dependencies

CentOS :

```shell
$ sudo yum install -y expect
```

Ubuntu :

```shell
$ sudo apt-get install tcl tk expect
```

Mac :

```shell
$ brew install expect
```


## Install GotoSSH

```shell
$ git clone https://github.com/MFrank2016/GotoSSH.git
$ cd GotoSSH
$ chmod a+x gotossh
$ sudo cp gotossh /usr/local/bin/
```

## Config

```shell
$ vim ~/.gotossh_config
server_name|ip|username|password|port|rely_server_no

[Server1]
command=tail -f -n 10 testlog.log

[scp]
log1=~/testlog.log
```

The config file consists of three parts.

The first part is the server base info:

```
server_name|ip|username|password|port|rely_server_no
```

For example:

```
JumpServer1|118.24.163.31|root|testpassword|22|0
OnlineServerB|111.231.59.85|root|testpassword2|22|1
```

The last column of the config means this server relies another server, so this shell will login that server first.(the no starts form `1`, so `0` means this server doesn’t rely others)

The second part is custom command, you could set any command here for each server.

```
[Server1]
command=tail -f -n 10 testlog.log
```

`Server1` means it's set for the first server.

`command` is the name of your command, that could be any name you like, and the actual command is behind the equals sign.

So you could use it by this way:

```
gotossh 1 command
```

And it will login the first server and excute your command.

Notice that, if your command needs a password, like 'scp root@xxxx:xxx xxx', you should add the pwd after the command.

For example:

```
[Server1]
command=scp root@111.231.59.85:/var/log/test-service/test-service.log ./test-server.log|testpassword2
```

The last part is the support of `scp` command:

```
[scp]
log1=~/testlog.log
log2=/var/log/test-service/test-service.log
```

`log1` and `log2` are the name you set, and the actual path of the file in server is behind the equals sign.

You could use it like this:

```
gotossh 1 scp log1
```

It will copy the remote file on the first server to your local computer.

```
gotossh 2 scp log2
```

It will login the first server, and copy that file from the second server, and then copy that file to your local computer.

## Example

```shell
$ vim ~/.gotossh_config
JumpServer1|118.24.163.31|root|testpassword|22|0
OnlineServerB|111.231.59.85|root|testpassword2|22|1

[Server1]
log=tail -f -n 20 testlog.log

[Server2]
log=tail -f -n 20 /var/log/test-service/test-service.log
cd=cd /var/log/test-service/

[scp]
log3=~/testlog.log
log4=/var/log/test-service/test-service.log
```

## Useage

```shell
$ gotossh
######################################################################################
#                                  [GOTO SSH]                                        #
#                                                                                    #
#                                                                                    #
# [1] test_server - 192.168.0.1:root                                                 #
# [2] online_server - 192.168.2.2:root                                               #
#                                                                                    #
#                                                                                    #
######################################################################################
Server Number:(Input Server Number Here)
```


```shell
gotossh 1
```


```shell
gotossh 2
```

```
gotossh 1 log
```

```
gotossh 2 log
```

```
gotossh 2 cd
```

```
gotossh 1 scp log3
```

```
gotossh 2 scp log4
```

<a name="chinese"></a>

## 说明

GotoSSH是一个一键登录SSH的脚本，可直接从跳板机登录到线上服务器，致力于帮助你提高工作效率。

这里有一些动态图，可以帮助你快速了解这个脚本能够做什么。

普通的一键登录:

![](https://i.loli.net/2019/03/29/5c9cf654b339b.gif)

一键登录跳板机，然后跳转登录线上服务器：

![](https://i.loli.net/2019/03/29/5c9cf6c81ad1f.gif)

![](https://i.loli.net/2019/03/29/5c9cf6ee38d18.gif)

一键登录跳板机查看指定日志：

![](https://i.loli.net/2019/03/29/5c9cf72b7b707.gif)

一键登录跳板机后跳转线上服务器查看指定日志：

![](https://i.loli.net/2019/03/29/5c9cf76aad6ac.gif)

然后是更加劲爆内容，一键从跳板机复制指定文件到本地：

![](https://i.loli.net/2019/03/29/5c9cf782c0db4.gif)

一键从生产环境复制指定文件到本地：

![](https://i.loli.net/2019/03/29/5c9cf7b506db0.gif)

![20190329003615.png](https://i.loli.net/2019/03/29/5c9cf80147c31.png)

## 安装依赖

CentOS :

```shell
$ sudo yum install -y expect
```

Ubuntu :

```shell
$ sudo apt-get install tcl tk expect
```

Mac :

```shell
$ sudo brew install expect
```

## 安装 GotoSSH

```shell
$ git clone https://github.com/MFrank2016/GotoSSH.git
$ cd GotoSSH
$ chmod a+x gotossh
$ sudo cp gotossh /usr/local/bin/
```

## 配置

```shell
$ vim ~/.gotossh_config
server_name|ip|username|password|port|rely_server_no

[Server1]
command=tail -f -n 10 testlog.log

[scp]
log1=~/testlog.log
```

配置文件由三部分组成。

第一部分是服务器的基本信息。

```
server_name|ip|username|password|port|rely_server_no
```

举个栗子：

```
JumpServer1|118.24.163.31|root|testpassword|22|0
OnlineServerB|111.231.59.85|root|testpassword2|22|1
```

最后一列是代表该服务器依赖于哪个服务器，如果该列的值设置为0，代表不依赖于其他服务器，否则代表需要先登录其他服务器后才能登录该服务器，目前暂时只支持二连跳，不支持多跳转。

第二部分是自定义命令，你可以在这里为每台服务器单独设置一些自定义命令。

```
[Server1]
command=tail -f -n 10 testlog.log
```

`Server1` 表示以下是为第一台服务器设置的命令，同理`Server2`则表示为第二台设置的命令。对于顺序没有要求，只要为需要设置自定义命令的服务器添加该选项即可。

`command` 是命令的名字，可以随意取名，最好简单一点，方便输入，等号后面是实际执行的命令。

举个栗子：

```
gotossh 1 command
```

只要你小手一点回车，脚本便会自动帮你登录到第一台服务器，然后执行上面的命令`tail -f -n 10 testlog.log`。

注意，如果你输入的命令需要密码的话，需要在命令后面把密码也带上，并且用`|`分隔。

举个栗子：

```
[Server1]
command=scp root@111.231.59.85:/var/log/test-service/test-service.log ./test-server.log|testpassword2
```

配置文件的最后一部分是对于`scp`命令的支持。

```
[scp]
log1=~/testlog.log
log2=/var/log/test-service/test-service.log
```

`log1` 和 `log2` 都是随意起的名字，后面是服务器上你想要复制的文件路径，配置好之后，你就可以这样使用：

```
gotossh 1 scp log1
```

它就会自动把第一台服务器上的`~/testlog.log`文件复制到你的本地。

```
gotossh 2 scp log2
```

这个操作就更厉害了，因为第二台服务器设置了对第一台服务器的依赖，所以它会先登录第一台服务器，然后再复制第二台服务器上的文件到第一台服务器上，最后，退出到本地，将第一台服务器上的复制品再拷贝到本地。

## 配置文件举例

```shell
$ vim ~/.gotossh_config
JumpServer1|118.24.163.31|root|testpassword|22|0
OnlineServerB|111.231.59.85|root|testpassword2|22|1

[Server1]
log=tail -f -n 20 testlog.log

[Server2]
log=tail -f -n 20 /var/log/test-service/test-service.log
cd=cd /var/log/test-service/

[scp]
log3=~/testlog.log
log4=/var/log/test-service/test-service.log
```

## 用法

```shell
$ gotossh
######################################################################################
#                                  [GOTO SSH]                                        #
#                                                                                    #
#                                                                                    #
# [1] test_server - 192.168.0.1:root                                                 #
# [2] online_server - 192.168.2.2:root                                               #
#                                                                                    #
#                                                                                    #
######################################################################################
Server Number:(Input Server Number Here)
```


```shell
gotossh 1
```


```shell
gotossh 2
```

```
gotossh 1 log
```

```
gotossh 2 log
```

```
gotossh 2 cd
```

```
gotossh 1 scp log3
```

```
gotossh 2 scp log4
```


