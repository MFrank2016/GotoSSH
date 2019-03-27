# GotoSSH

- [English Version](#english)
- [中文版](#chinese)

<a name="english"></a>

## Description

GotoSSH is committed to helping you improve work efficiency.



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
$ sudo brew install expect
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
```

The last column of the config means this server relies another server, so this shell will login that server first.(the no starts form `1`, so `0` means this server doesn’t rely others)



## Example

```shell
$ vim ~/.gotossh_config
test_server|192.168.0.1|root|password|22|0
online_server|192.168.2.2|root|password|22|1
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

OR

```shell
gotossh 1
```

OR

```shell
gotossh 2
```

It will login server1 first, and then login server2 by this way.



<a name="chinese"></a>

## 说明

GotoSSH是一个一键登录SSH的脚本，可直接从跳板机登录到线上服务器，致力于帮助你提高工作效率。



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
```

最后一列是代表该服务器依赖于哪个服务器，如果该列的值设置为0，代表不依赖于其他服务器，否则代表需要先登录其他服务器后才能登录该服务器，目前暂时只能从A跳转到B，不支持多跳转，感觉没有必要，如果有需要，把脚本稍微改改就行了。



## 举个栗子

```shell
$ vim ~/.gotossh_config
test_server|192.168.0.1|root|password|22|0
online_server|192.168.2.2|root|password|22|1
```



## 使用说明

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

OR

```shell
gotossh 1
```

OR

```shell
gotossh 2
```

因为配置文件里设置了服务器2依赖于服务器1，所以会先登录服务器1，然后再登录服务器2。

