# docker + v2ray-plugin + shadowsocks + nginx + cloudflare
仅供学习 docker
使用docker-compose 一键搭建 代理服务，并获得一个静态博客。

```
  your.domain.com 
  |
  └--> cloudflare CDN 
          |
          |
          |         ┌--tls--> shadowsocks ---> v2ray-plugin
          V         |
     docker ━━━━━>nginx
                    |
                    └--tls-->  html（blog）  
```

不套cf,建议选择（docker + v2ray + caddy )，caddy 自动tls申请非常方便！



## Usage
安装 docker-compose 最新版本
 
command + R repalce sg.domain.com to your domain.

$ git clone && cd v2-ss-nginx

generate and save your cf ssl to: cert -> pem/domain.pem  key ->pem/domian.key

confirm 80, 443 not in using.

$ docker-compose up -d

$ docker ps #成功
```sh
root@domain# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                      NAMES
70f1eadf146c        ss-v2-webserver     "nginx -g 'daemon of…"   7 days ago          Up 7 days           0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   v2-ss-nginx_webserver_1
f763eaaadd19        ss-v2ray            "/bin/sh -c 'ss-serv…"   7 days ago          Up 7 days           0.0.0.0:1088->1088/tcp                     v2-ss-nginx_ss-v2ray_1
```

## 为了性能 ，network_mode最好能用host模式，但是我是在Mac上测试的，Mac 的docker 不支持 host模式。只能让docker虚拟一个网卡，做桥接模式。
```network_mode: "host"```
## 并不建议在vps 里面用着一套东西，本身是虚拟机，v2ray 又套在docker里，docker还要虚拟一个网卡，而v2ray服务又是跟网络密不可分的（除非基于容器云搭建。
