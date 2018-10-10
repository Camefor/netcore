# .net core

使用 Nginx 在 Linux 上托管 ASP.NET Core
https://docs.microsoft.com/zh-cn/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-2.1&tabs=aspnetcore2x

**相关注意事项**

.net core程序无论是调试还是发布版本，都必须在程序目录下运行命令，否则可能会出现静态资源文件无法访问的问题
 

**启动并监听Web服务**
systemd 可用于创建服务文件以启动和监视基础 Web 应用。 systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。

* 创建服务文件
```sh
$ sudo vim /etc/systemd/system/kestrel-lottery.service
```

* 服务文件内容如下
```
[Unit]
Description=Lottery

[Service]
WorkingDirectory=/home/colin/projs/lottery
ExecStart=/usr/bin/dotnet /home/colin/projs/lottery/Colin.Lottery.WebApp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
SyslogIdentifier=dotnet-lottery
User=colin
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

* 启动服务
```sh
# 启用服务
$ systemctl enable kestrel-lottery.service

# 启动服务
$ systemctl start kestrel-lottery.service

# 查看服务状态
$ systemctl status kestrel-lottery.service

# 停止服务
$ systemctl stop kestrel-lottery.service
```
