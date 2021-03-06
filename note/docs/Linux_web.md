#Linux中配置静态网络连接
许多新的Linux发行版都带有网络管理工具，可以帮你自动连接到无线网络，但是能够为Linux机器建立静态网络不是更好吗，该笔记将展示如何使用不同的Linux工具检查CentOs机器的网络连接，如何使用nmcli工具添加静态网络配置。

##检查网络连接
ping 命令是一个众所周知的的程序，可以快速的检查网络的连通性：

```
ping -c3 opensource.com
```

其中 -c3 选项表示你只 ping 三次

![ping](https://wendaoshuai66.github.io/study/note/images/ping1.png)

如果连接到了互联网，将会收到类似的数据包相应

##检查连接信息

可以用ip add 命令检查网络信息

![ping](https://wendaoshuai66.github.io/study/note/images/ping2.png)

运行此命令显示设备信息和ip地址等，稍后将要用到，因此记住

##检查网络信息

通过 输入一下命令，可以在 /etc/sysconfig/network-scripts中找到网络信息

```

ls /etc/sysconfig/network-scripts
```
![ping](https://wendaoshuai66.github.io/study/note/images/ping3.png)


该截图 显示了ifcfg-ens33 和 ifcfg-lo，但这些取决于你运行的Linux以及设备的设置方式

##显示可用的连接

可以用nmcli 工具显示当前网络，输入以下命令：

```

nmcli con show
```
![ping](https://wendaoshuai66.github.io/study/note/images/ping4.png)


此截图显示一台设备处于活动状态：ens33

##检查网络连接是否已打开

用上面的ping可以命令检查你是否可以接受数据包，但现在我们要通过 systemctl 命令调用network来监视，更新网络状态和排除故障


```
systemctl status network
```
![ping](https://wendaoshuai66.github.io/study/note/images/ping5.png)

如果网络支持程序没有问题，那么运行此命令是你会看到active

##添加静态网络连接


现在准备添加静态网落连接。使用此步骤中2从ip  add中获取的设备名称，输入以下添加新连接：

```
nmcli con add con-name "SomeName"  ifname YOUR__DEVICE autoconnect yes type YOUR_CONNECTION_TYPE
```

![ping](https://wendaoshuai66.github.io/study/note/images/ping6.png)


##验证连接是否已被添加到网络脚本路径中

可以用nmcli工具修改新的连接信息

```
nmcli con mod
```
这个命令实际修改了/etc/sysconfig/network-scripts目录下的网络配置脚本，这也是修改连接信息的另一种方法。
通过以下命令

```
ls /etc/sysconfig/network-scripts
```
![ping](https://wendaoshuai66.github.io/study/note/images/ping7.png)

##确认你可以看到连接

检查MyLikeCafe是否为可见的可用的连接，使用以下命令

```
nmclie con up Some_CONNECTION NAME
```

也可以用一下命令将其关闭：

```
nmcli con down Some_CONNECTION_NAME
```

##将连接修改为静态

用文本编辑器（如Vim Emacs 或Nano）打开  /etc/sysconfig/network-scripts/Some_CONNECTION_NAME,

把连接配置为静态，需要修改一个参数，并添加三个参数：

1.修改BOOTPROTO为static

2.添加IPADDR及你要设置的静态IP地址，可以通过ip add命令看到

3.添加NETMASK。这是子网掩码，可以通过ip add找到

4.添加GATEWAY。这个是默认的网关的ip地址。可以通过ip add找到


你可能需要添加DNS，PREFIX或其他信息，具体情况取决于你的网络和计算机设置
完成后重启

```
systemctl restart network
```

检查状态

```
systemctl status network
```

##确认连接处于活动状态

```
nmcli con show
```