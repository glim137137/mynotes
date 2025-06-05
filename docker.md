# Docker

**文章参考**：[Docker 官方文档](https://docs.docker.com/)、[Docker Hub](https://hub.docker.com/)

[TOC]

## 介绍

### 什么是 Docker

Docker 是一个开源的容器化平台，用于开发、部署和运行应用程序。它通过容器技术将应用程序及其依赖项打包在一起，确保应用程序在不同环境（开发、测试、生产）中以一致的方式运行。Docker 容器轻量、快速且可移植，适用于大多数操作系统，包括 Linux、Windows 和 macOS。

Docker 基于容器化技术，核心是 Linux 容器（LXC）和 cgroups，但通过其用户友好的工具和生态系统大大简化了容器管理。相比传统的虚拟机，Docker 容器共享主机操作系统的内核，减少了资源开销，提高了性能。

如果你熟悉虚拟机或传统的应用程序部署方式，Docker 的工作方式可能需要适应。Docker 不是“所见即所得”的工具，而是通过配置文件（Dockerfile）和命令行工具（Docker CLI）来定义和操作容器。用户专注于定义应用程序的运行环境，而不是手动配置服务器。

一个 Docker 应用程序通常由一个 `Dockerfile`（定义容器构建过程的脚本）和镜像（image）组成。镜像可以通过 Docker CLI 构建，并运行在容器中。最终，容器可以在本地或云端运行，支持多种部署环境。

### 一些概念

要使用 Docker，你需要安装 Docker 引擎。官方支持的发行版包括 [Docker Desktop](https://www.docker.com/products/docker-desktop/)（适用于 Windows 和 macOS）和 [Docker Engine](https://docs.docker.com/engine/)（适用于 Linux）。Docker Desktop 包含 Docker CLI、Docker Compose 和图形化界面，而 Docker Engine 是轻量级 CLI 工具，适合服务器环境。

Docker 有以下核心组件：
- **Dockerfile**：一个文本文件，包含构建 Docker 镜像的指令。
- **镜像（Image）**：只读模板，包含应用程序、依赖和运行时环境。
- **容器（Container）**：镜像的运行实例，隔离运行应用程序。
- **Docker Hub**：官方镜像仓库，用户可以拉取或推送镜像。
- **Docker Compose**：用于定义和运行多容器应用的工具，通过 YAML 文件描述服务、网络和卷。

推荐使用 Docker Desktop 进行本地开发，配合 Visual Studio Code 或其他支持 Docker 插件的编辑器。Docker CLI 是主要操作工具，适用于所有环境。

扩展阅读：[Docker 架构概述](https://docs.docker.com/get-started/overview/)。

### 环境配置

对于 Windows 和 macOS 用户，推荐安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)。国内用户可通过 [清华大学 TUNA 镜像站](https://mirrors.tuna.tsinghua.edu.cn/) 下载 Docker Desktop 的安装包，位于“应用软件”标签下的“容器化技术”分类。

对于 Linux 用户，可通过官方脚本安装 Docker Engine：
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
安装后，建议将当前用户添加到 `docker` 组以避免每次使用 `sudo`：
```bash
sudo usermod -aG docker $USER
```

安装完成后，运行以下命令验证：
```bash
docker --version
docker run hello-world
```

## 基本操作

### 基本要素

- 安装 Docker Desktop 或 Docker Engine。
- 打开终端，运行 `docker --version` 检查版本。
- 创建一个 `Dockerfile`，示例：
```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y python3
CMD ["python3", "--version"]
```
- 保存文件为 `Dockerfile`，在同一目录下运行：
```bash
docker build -t my-python-image .
```
- 运行容器：
```bash
docker run my-python-image
```

`FROM` 指定基础镜像，`RUN` 执行构建时的命令，`CMD` 定义容器启动时的默认命令。`-t` 为镜像命名，`.` 表示当前目录。

### 处理问题

如果构建或运行失败，检查终端输出：
- **错误信息**：如镜像拉取失败，检查网络或配置镜像加速器（国内用户推荐 [阿里云镜像加速](https://cr.console.aliyun.com/)）。
- **语法错误**：检查 `Dockerfile` 语法，常见错误包括缺少 `FROM` 或命令拼写错误。
- 运行 `docker logs <container_id>` 查看容器日志，`docker ps -a` 查看容器状态。

### 容器管理

Docker 提供多种命令管理容器：
- `docker ps`：列出运行中的容器。
- `docker ps -a`：列出所有容器（包括已停止）。
- `docker stop <container_id>`：停止容器。
- `docker rm <container_id>`：删除容器。

示例：
```bash
docker run -d --name my-container my-python-image
docker stop my-container
docker rm my-container
```

`-d` 表示后台运行，`--name` 为容器命名。

### 镜像管理

镜像可以通过 `docker build` 创建，或从 Docker Hub 拉取：
```bash
docker pull nginx:latest
```
删除镜像：
```bash
docker rmi nginx:latest
```

### 卷与网络

Docker 卷用于持久化数据：
```bash
docker volume create my-volume
docker run -v my-volume:/data my-image
```
`-v` 将卷挂载到容器内的 `/data` 目录。

网络配置允许容器通信：
```bash
docker network create my-network
docker run --network my-network --name app1 my-image
```

### 生成 Compose 文件

使用 Docker Compose 管理多容器应用。创建 `docker-compose.yml`：
```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: example
```
运行：
```bash
docker-compose up -d
```

`docker-compose.yml` 定义服务、端口映射和环境变量。`-d` 表示后台运行。

## 高级功能

### 中间件支持

Docker 支持多种中间件（如 MySQL、Redis）通过官方镜像快速部署。例如：
```bash
docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=example mysql:8.0
```

### 构建优化

优化 `Dockerfile` 减少构建时间：
- 使用多阶段构建：
```dockerfile
FROM node:16 AS builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx:latest
COPY --from=builder /app/build /usr/share/nginx/html
```
- 缓存层：合理排序命令，避免重复安装依赖。

### 网络与安全

为容器配置网络隔离：
```bash
docker network create --driver bridge my-secure-network
```
设置容器资源限制：
```bash
docker run --memory="512m" --cpus="0.5" my-image
```

### 日志与监控

查看容器日志：
```bash
docker logs <container_id>
```
实时监控：
```bash
docker stats
```

## 实践

尝试以下任务：
1. 创建一个 `Dockerfile`，基于 `python:3.9`，安装 `flask` 并运行一个简单的 Web 应用。
2. 使用 Docker Compose 部署一个包含 Nginx 和 Redis 的多容器应用。
3. 配置卷以持久化 Redis 数据。

参考 [Docker 官方教程](https://docs.docker.com/get-started/) 或 [源代码](https://github.com/docker/docker.github.io) 获取帮助。