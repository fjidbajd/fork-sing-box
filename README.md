# 【Sing-box 全家桶】

* * *




* * *
## 1.更新信息
2025.04.25 v1.2.17 1. Added the ability to change CDNs online using [sb -d]; 2. Change GitHub proxy; 3. Optimize code; 1. 新增使用 [sb -d] 在线更换 CDN 功能; 2. 更改 GitHub 代理; 3. 优化代码

2025.04.06 v1.2.16 Use OpenRC on Alpine to replace systemctl (Python3-compatible version); 在 Alpine 系统中使用 OpenRC 取代兼容 Python3 的 systemctl 实现

2025.04.05 v1.2.15 Supports output for clients such as Shadowrocket, Clash Mihomo, and Sing-box; 支持小火箭、Clash Mihomo、Sing-box 客户端输出

2025.03.23 v1.2.14 Added support for the AnyTLS protocol. Thanks to [Betterdoitnow] for providing the configuration; 新增对 AnyTLS 协议的支持，感谢 [Betterdoitnow] 提供的配置



## 2.项目特点:

* 一键部署多协议，可以单选、多选或全选 ShadowTLS v3 / XTLS Reality / Hysteria2 / Tuic V5 / ShadowSocks / Trojan / Vmess + ws / Vless + ws + tls / H2 Reality / gRPC Reality / AnyTLS, 总有一款适合你
* 所有协议均不需要域名，可选 Cloudflare Argo Tunnel 内网穿透以支持传统方式为 websocket 的协议
* 节点信息输出到 V2rayN / Clash Verge / 小火箭 / Nekobox / Sing-box (SFI, SFA, SFM)，订阅自动适配客户端，一个订阅 url 走天下
* 自定义端口，适合有限开放端口的 nat 小鸡
* 内置 warp 链式代理解锁 chatGPT
* 智能判断操作系统: Ubuntu 、Debian 、CentOS 、Alpine 和 Arch Linux,请务必选择 LTS 系统
* 支持硬件结构类型: AMD 和 ARM，支持 IPv4 和 IPv6
* 无交互极速安排模式: 一个回车完成 11 个协议的安装


## 3.Sing-box for VPS 运行脚本:

* 首次运行
```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/sing-box/main/sing-box.sh)
```

* 再次运行
```
sb
```

  | Option 参数      | Remark 备注 |
  | --------------- | ------ |
  | -c              | Chinese 中文 |
  | -e              | English 英文 |
  | -u              | Uninstall 卸载 |
  | -n              | Export Nodes list 显示节点信息 |
  | -p <start port> | Change the nodes start port 更改节点的起始端口 |
  | -d              | Change CDN 更换 CDN |
  | -s              | Stop / Start the Sing-box service 停止/开启 Sing-box 服务 |
  | -a              | Stop / Start the Argo Tunnel service 停止/开启 Argo Tunnel 服务 | 
  | -v              | Sync Argo Xray to the newest 同步 Argo Xray 到最新版本 |
  | -b              | Upgrade kernel, turn on BBR, change Linux system 升级内核、安装BBR、DD脚本 |
  | -r              | Add and remove protocols 添加和删除协议 |



## 5.Token Argo Tunnel 方案设置任意端口回源以使用 cdn
详细教程: [群晖套件：Cloudflare Tunnel 内网穿透中文教程 支持DSM6、7](https://imnks.com/5984.html)

<img width="1510" alt="image" src="https://github.com/fscarmen/sba/assets/62703343/bb2d9c43-3585-4abd-a35b-9cfd7404c87c">

<img width="1638" alt="image" src="https://github.com/fscarmen/sing-box/assets/62703343/a4868388-d6ab-4dc7-929c-88bc775ca851">


## 6.Vmess / Vless 方案设置任意端口回源以使用 cdn
举例子 IPv6: vmess [2a01:4f8:272:3ae6:100b:ee7a:ad2f:1]:10006
<img width="1052" alt="image" src="https://github.com/fscarmen/sing-box/assets/62703343/bc2df37a-95c4-4ba0-9c84-5d9c745c3a7b">

1. 解析域名
<img width="1605" alt="image" src="https://github.com/fscarmen/sing-box/assets/62703343/8f38d555-6294-493e-b43d-ff0586c80d61">

2. 设置 Origin rule
<img width="1556" alt="image" src="https://github.com/fscarmen/sing-box/assets/62703343/164bf255-a6be-40bc-a724-56e13da7a1e6">


## 7.Docker 和 Docker compose 安装

### 说明:
* 支持三种 Argo 类型隧道: 临时 (不需要域名) / Json / Token
* 需要20个连续可用的端口，以 `START_PORT` 开始第一个

<details>
    <summary> Docker 部署（点击即可展开或收起）</summary>
<br>

```
docker run -dit \
    --pull always \
    --name sing-box \
    -p 8800-8820:8800-8820/tcp \
    -p 8800-8820:8800-8820/udp \
    -e START_PORT=8800 \
    -e SERVER_IP=123.123.123.123 \
    -e XTLS_REALITY=true \
    -e HYSTERIA2=true \
    -e TUIC=true \
    -e SHADOWTLS=true \
    -e SHADOWSOCKS=true \
    -e TROJAN=true \
    -e VMESS_WS=true \
    -e VLESS_WS=true \
    -e H2_REALITY=true \
    -e GRPC_REALITY=true \
    -e ANYTLS=true \
    -e UUID=20f7fca4-86e5-4ddf-9eed-24142073d197 \
    -e CDN=www.csgo.com \
    -e NODE_NAME=sing-box \
    -e ARGO_DOMAIN=sb.argo.com \
    -e ARGO_AUTH='{"AccountTag":"9cc9e3e4d8f29d2a02e297f14f20513a","TunnelSecret":"6AYfKBOoNlPiTAuWg64ZwujsNuERpWLm6pPJ2qpN8PM=","TunnelID":"1ac55430-f4dc-47d5-a850-bdce824c4101"}' \
    fscarmen/sb
```
</details>

<details>
    <summary> Docker Compose 部署（点击即可展开或收起）</summary>
<br>

```
version: '3.8'
networks:
    sing-box:
        name: sing-box
services:
    sing-box:
        image: fscarmen/sb
        pull_policy: always
        container_name: sing-box
        restart: always
        networks:
            - sing-box
        ports:
            - "8800-8820:8800-8820/tcp"
            - "8800-8820:8800-8820/udp"
        environment:
            - START_PORT=8800
            - SERVER_IP=123.123.123.123
            - XTLS_REALITY=true
            - HYSTERIA2=true
            - TUIC=true
            - SHADOWTLS=true
            - SHADOWSOCKS=true
            - TROJAN=true
            - VMESS_WS=true
            - VLESS_WS=true
            - H2_REALITY=true
            - GRPC_REALITY=true
            - ANYTLS=true
            - UUID=20f7fca4-86e5-4ddf-9eed-24142073d197 
            - CDN=www.csgo.com
            - NODE_NAME=sing-box
            - ARGO_DOMAIN=sb.argo.com
            - ARGO_AUTH=eyJhIjoiOWNjOWUzZTRkOGYyOWQyYTAyZTI5N2YxNGYyMDUxM2EiLCJ0IjoiOGNiZDA4ZjItNGM0MC00OGY1LTlmZDYtZjlmMWQ0YTcxMjUyIiwicyI6IllXWTFORGN4TW1ZdE5HTXdZUzAwT0RaakxUbGxNMkl0Wm1VMk5URTFOR0l4TkdKayJ9
```
</details>


### 常用指令
| 功能 | 指令 |
| ---- | ---- |
| 查看节点信息 | `docker exec -it sing-box cat list` |
| 查看容器日志 | `docker logs -f sing-box` |
| 更新 Sing-box 版本 | `docker exec -it sing-box bash init.sh -v` |
| 查看容器内存,CPU，网络等资源使用情况 | `docker stats sing-box` |
| 暂停容器 | docker: `docker stop sing-box`</br> compose: `docker-compose stop` |
| 停止并删除容器 | docker: `docker rm -f sing-box`</br> compose: `docker-compose down` |
| 删除镜像 | `docker rmi -f fscarmen/sb:latest` |


### 用户可以通过 Cloudflare Json 生成网轻松获取: https://fscarmen.cloudflare.now.cc

<img width="784" alt="image" src="https://github.com/fscarmen/sba/assets/62703343/fb7c6e90-fb3e-4e77-bcd4-407e4660a33c">

如想手动，可以参考，以 Debian 为例，需要用到的命令，[Deron Cheng - CloudFlare Argo Tunnel 试用](https://zhengweidong.com/try-cloudflare-argo-tunnel)


### Argo Token 的获取

详细教程: [群晖套件：Cloudflare Tunnel 内网穿透中文教程 支持DSM6、7](https://imnks.com/5984.html)

<img width="1510" alt="image" src="https://github.com/fscarmen/sba/assets/62703343/bb2d9c43-3585-4abd-a35b-9cfd7404c87c">

<img width="1616" alt="image" src="https://github.com/fscarmen/sing-box/assets/62703343/ecb844be-1e93-4208-bb7c-6b00b9d1f00a">


### 参数说明
| 参数 | 是否必须 | 说明 |
| --- | ------- | --- |
| -p /tcp | 是 | 宿主机端口范围:容器 sing-box 及 nginx 等 tcp 监听端口 |
| -p /udp | 是 | 宿主机端口范围:容器 sing-box 及 nginx 等 udp 监听端口 |
| -e START_PORT | 是 | 起始端口 ，一定要与端口映射的起始端口一致 |
| -e SERVER_IP | 是 | 服务器公网 IP |
| -e XTLS_REALITY | 是 |    true 为启用 XTLS + reality，不需要的话删除本参数或填 false |
| -e HYSTERIA2 | 是 |       true 为启用 Hysteria v2 协议，不需要的话删除本参数或填 false |
| -e TUIC | 是 |            true 为启用 TUIC 协议，不需要的话删除本参数或填 false |
| -e SHADOWTLS | 是 |       true 为启用 ShadowTLS 协议，不需要的话删除本参数或填 false |
| -e SHADOWSOCKS | 是 |     true 为启用 ShadowSocks 协议，不需要的话删除本参数或填 false |
| -e TROJAN | 是 |          true 为启用 Trojan 协议，不需要的话删除本参数或填 false |
| -e VMESS_WS | 是 |        true 为启用 VMess over WebSocket 协议，不需要的话删除本参数或填 false |
| -e VLESS_WS | 是 |        true 为启用 VLess over WebSocket 协议，不需要的话删除本参数或填 false |
| -e H2_REALITY | 是 |      true 为启用 H2 over reality 协议，不需要的话删除本参数或填 false |
| -e GRPC_REALITY | 是 |    true 为启用 gRPC over reality 协议，不需要的话删除本参数或填 false |
| -e ANYTLS | 是 |          true 为启用 AnyTLS 协议，不需要的话删除本参数或填 false |
| -e UUID | 否 | 不指定的话 UUID 将默认随机生成 |
| -e CDN | 否 | 优选域名，不指定的话将使用 www.csgo.com |
| -e NODE_NAME | 否 | 节点名称，不指定的话将使用 sing-box |
| -e ARGO_DOMAIN | 否 | Argo 固定隧道域名 , 与 ARGO_DOMAIN 一并使用才能生效 |
| -e ARGO_AUTH | 否 | Argo 认证信息，可以是 Json 也可以是 Token，与 ARGO_DOMAIN 一并使用才能生效，不指定的话将使用临时隧道 |


