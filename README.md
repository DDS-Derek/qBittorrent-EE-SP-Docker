# qBittorrent-EE-SP-Docker

# 本镜像为qBittorrent增强快较版，非官方qBittorrent，使用者请自行承担风险！

![Docker Pulls](https://img.shields.io/docker/pulls/ddsderek/qbittorrent_ee_sp.svg?style=for-the-badge&label=pulls&logo=docker)

由 nevinee 大佬的 qBittorrent 镜像改编的 qBittorrent 增强快较版 镜像。

此项目功能与使用方法和`nevinee/qbittorrent`一致，故详细功能和使用教程[点击这里](https://evine.win/p/docker-install-qbittorrent/)查看。

## 架构

| Architecture | Tag            |
| :----------: | :------------: |
| x86-64       | latest   |
| arm64        | latest |
| arm32        | latest |

## 标签

- **`4.x.x` , `latest`**: 标签以纯数字版本号命名，这是qBittorrentee正式发布的稳定版，其中最新的版本额外增加`latest`标签。

## 部署

**qBittorrent-EE-SP**

```yaml
version: "2.0"
services:
  qbittorrentee:
    image: ddsderek/qbittorrent_ee_sp:latest
    container_name: qbittorrent_ee_sp
    restart: always
    tty: true
    network_mode: bridge
    hostname: qbittorrent_ee_sp
    volumes:
      - ./data:/data      # 配置保存目录
    tmpfs:
      - /tmp
    environment:          # 下面未列出的其他环境变量请根据环境变量清单自行添加
      - WEBUI_PORT=8080   # WEBUI控制端口，可自定义
      - BT_PORT=34567     # BT监听端口，可自定义
      - PUID=1000         # 输入id -u可查询，群晖必须改
      - PGID=100          # 输入id -g可查询，群晖必须改
    ports:
      - 8080:8080        # 冒号左右一致，必须同WEBUI_PORT一样，本文件中的3个8080要改一起改
      - 34567:34567      # 冒号左右一致，必须同BT_PORT一样，本文件中的5个34567要改一起改
      - 34567:34567/udp  # 冒号左右一致，必须同BT_PORT一样，本文件中的5个34567要改一起改
    #security_opt:       # armv7设备请解除本行和下一行的注释
      #- seccomp=unconfined
```
