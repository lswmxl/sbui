# x-ui

支持多协议多用户的 xray 面板

# 功能介绍

- 系统状态监控
- 支持多用户多协议，单端口多用户，网页可视化操作
- 支持的协议：vmess、vless、trojan、shadowsocks、dokodemo-door、socks、http
- 支持 vless / trojan reality
- 支持配置更多传输配置
- 流量统计，限制流量，限制到期时间
- 可自定义 xray 配置模板
- 支持 https 访问面板（自备域名 + ssl 证书）
- 支持一键SSL证书申请且自动续签
- 更多高级配置项，详见面板

# 安装 & 升级

```
bash <(wget -qO- https://5th.pp.ua/https://raw.githubusercontent.com/lswmxl/sbui/refs/heads/main/install_CN.sh)
```

## 手动安装&升级

1. 首先从项目中下载最新的压缩包，一般选择 `amd64`架构
2. 然后将这个压缩包上传到服务器的 `/root/`目录下，并使用 `root`用户登录服务器

> 如果你的服务器 cpu 架构不是 `amd64`，自行将命令中的 `amd64`替换为其他架构

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## 使用docker安装

> 此 docker 教程与 docker 镜像由[Chasing66](https://github.com/Chasing66)提供

1. 安装docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. 安装x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    misakablog/x-ui:latest
```

> Build 自己的镜像

```shell
docker build -t x-ui .
```

## TG 机器人使用


- Tg机器人Token
- Tg机器人ChatId
- Tg机器人周期运行时间，采用crontab语法  

参考语法：
- 30 * * * * * //每一分的第30s进行通知
- @hourly      //每小时通知
- @daily       //每天通知（凌晨零点整）
- @every 8h    //每8小时通知  

TG通知内容：
- 节点流量使用
- 面板登录提醒
- 节点到期提醒
- 流量预警提醒  



## 建议系统

- CentOS 7+
- Ubuntu 16+
- Debian 8+
