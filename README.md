# SmokePing 一键脚本

[SmokePing](https://oss.oetiker.ch/smokeping) 是由 RRDtool 的作者 Tobi Oetiker 开发的一款监控网络状态和稳定性的开源软件。使用脚本安装后，SmokePing 会定时向目标发送 TCP 数据包，并对返回值进行测量和记录，通过 RRDtool 制图程序图形化地展示在各个时段内网络的延迟、抖动和丢包率，帮助我们更清楚、更直观地了解服务器的网络状况。

本脚本会使 SmokePing 运行在 Caddy 上，与其他 WEB 服务隔离。

本脚本修改自[jiuqi9997大佬的脚本](https://github.com/jiuqi9997/smokeping)

## 修改内容

1.  在其基础上添加了教育网监控,同时改为下载最新版smokeping与caddy(用了`jq`实现获取最新版本所以脚本加了`jq`的安装);
2.  同时提供了[启动运行脚本](https://raw.githubusercontent.com/Xiefengshang/smokeping/main/start.sh),[停止运行脚本](https://raw.githubusercontent.com/Xiefengshang/smokeping/main/stop.sh),[重启脚本](https://raw.githubusercontent.com/Xiefengshang/smokeping/main/restart.sh),[卸载脚本](https://raw.githubusercontent.com/Xiefengshang/smokeping/main/uninstall.sh);
3.  获取本机ip改为[ip.sb](https://ip.sb)网站;

目前支持的 Linux 发行版：
```
Debian 9+
Ubuntu 18+
CentOS 7+
```
**支持ARM架构，理论来说只要caddy支持的架构都能用**
## 安装

**由于是编译安装，所以在安装期间需要大量占用CPU并且需要一定时间，大约3-5min左右**

**低内存小鸡存在编译安装卡住/异常退出的可能，建议开swap，OVZ的机器只能多试几次了，我的dedipath OVZ跑了3次。实际安装过程中最高占用为300M+，所以尽量在剩余内存>=300M的情况下运行此脚本**

```
bash -c "$(curl -L https://github.com/Xiefengshang/smokeping/raw/main/main.sh)"
```

如果出现 `command not found` 请执行 `apt-get install curl -y` 或 `yum install curl -y`。

## 配置
脚本自动为 SmokePing 进行配置，可以自行按需修改。
SmokePing 主配置文件（包括目标节点）为 `/usr/local/smokeping/etc/config`，此文件的结构及其修改请查阅相关教程，附上[示例](https://oss.oetiker.ch/smokeping/doc/smokeping_examples.en.html)。
**如果图片生成的中文乱码，则运行如下代码**
`apt-get install ttf-wqy-zenhei -y` or `yum install wqy-zenhei-fonts.noarch -y`
## 停止/重启/卸载SmokePing相关文件
1. 启动运行
```
bash -c "$(curl -L https://raw.githubusercontent.com/Xiefengshang/smokeping/main/start.sh)"
```
2. 停止运行
```
bash -c "$(curl -L https://raw.githubusercontent.com/Xiefengshang/smokeping/main/stop.sh)"
```
3. 重启
```
bash -c "$(curl -L https://raw.githubusercontent.com/Xiefengshang/smokeping/main/restart.sh)"
```
4. 卸载
```
bash -c "$(curl -L https://raw.githubusercontent.com/Xiefengshang/smokeping/main/uninstall.sh)"
```
