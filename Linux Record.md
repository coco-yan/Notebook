## 基础知识

- 前端总线速度

  CPU内的内存控制芯片与主存储器间的传输速

- 字组大小

  CPU每次能够处理的数据

- BIOS CMOS

- I/O地址



## arch安装问题记录

### pacman 语法

```shell
> pacman -Syu				#升级整个系统
> pacman -Qdt				#要罗列所有不再作为依赖的软件包(孤立orphans)
> pacman -Qet				#要罗列所有明确安装而且不被其它包依赖的软件包
```

```shell
> pactree pack_name			 #要显示软件包的依赖树
```

```shell
pacman 将下载的软件包保存在 /var/cache/pacman/pkg/ 并且不会自动移除旧的和未安装版本的软件包，因此需要手动清理

> pacman -Sc				#仅会保留软件包的当前有效版本，旧版本的软件包被清理
```

![目录功能](C:\Users\SHUHAN\Desktop\testgit\pic\2.png)



## Ubuntu问题

```shell
apt-get purge pakege
#删除已安装包（不保留配置文件)。
#如软件包a，依赖软件包b，则执行该命令会删除a，而且不保留配置文件
```

开机启动项：

```shell
systemctl list-unit-files | grep .......
```



## 云主传输文件

### 向服务器传输文件夹内的所有文件

```shell
scp -r local_dir username@servername:remote_dir
#例子
scp -r test user@192.168.0.101:/home/data
```

### 从服务器上下载整个目录

```shell
scp -r username@servername:/home/remote_dir /local_dir
```

