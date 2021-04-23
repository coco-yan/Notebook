## frps 反向代理与内网穿透

---

frp分为frps（server）和frpc（client）两个包 ，其中前者安装到我们的云服务器上，后者安装在需要被外网访问到的各个设备上

**云服务器端：frps.ini**

```shell
[common]
bind_port = 7000 # frp服务的端口号，可以自己定
dashboard_port = 7500 # frp的web界面的端口号
dashboard_user = user # web界面的登陆账户，自己修改
dashboard_pwd = pass # web界面的登陆密码，自己修改
authentication_method = token
token = xxxxx # frp客户端连接时的密码，自己修改
```

保存配置后，使用该命令启动：

```shell
./frps -c ./frps.ini
# 前面加上nohup似乎能在后台运行
```

**客户端：frpc.ini**

```shell
[common]
server_addr = xx.xx.xx.xx # 你的云服务器的公网ip
authentication_method = token
token = xxxxx # 刚刚配置的frp连接密码 
server_port = 7000 # 刚刚配置的frp服务端口

[Fusion-ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 20022

[Fusion-rdp]
type = tcp
local_ip = 127.0.0.1
local_port = 3389
remote_port = 23389
```

**通过上面的脚本就可以把对于云服务器特定端口的访问给重定向到本地服务器的某个端口了，简单地讲就是：假如我用SSH客户端访问 `[云服务器ip]:20022`，就可以经过反向代理直接访问到`[本地的训练服务器ip]:22`；同理需要连接远程桌面的话，只需要访问`[云服务器ip]:23389`就可以了。**

**当然你也可以修改脚本添加更多映射~**

3. 添加开机自动启动的脚本，新建一个文件内容如下：

文件名`/etc/systemd/system/frpc.service`，注意修改其中的路径：

```shell
[Fusion]
Description=Frp Server Daemon
After=syslog.target network.target
Wants=network.target
​
[Service]
Type=simple
ExecStart=/usr/local/bin/frp/frpc -c /usr/local/bin/frp/frpc.ini # 修改为你的frp实际安装目录
ExecStop=/usr/bin/killall frpc
#启动失败1分钟后再次启动
RestartSec=1min
KillMode=control-group
#重启控制：总是重启
Restart=always
​
[Install]
WantedBy=multi-user.target
```

然后执行以下命令启用脚本：

```shell
sudo systemctl enable frpc.service
sudo systemctl start frpc.service
sudo systemctl status frpc.service #查看状态
```

