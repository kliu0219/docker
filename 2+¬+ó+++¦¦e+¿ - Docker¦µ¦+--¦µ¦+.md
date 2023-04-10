> 该文档是 markdown 格式，vscode（需要安装插件）、pycharm 都能看，或者下一个 [typora](https://typora.io/)


cpython3.9 开始支持 apple silicon 的 mac

> [apple silicon 的 mac 如何安装新版本 cpython 解释器？](https://segmentfault.com/a/1190000042540277)


所以，下面的 cpython version 选择 3.9+ 


# 前言

## 起因

原本该课程提供的统计教学环境由 vagrant + vbox 搭建，但是随着 mac 全面转向 arm，而 vbox 又不支持 arm，所以，原来的 vagrant 教程不再适合 apple silicon 的 mac。

好在有 docker 来帮我们这些 apple silicon 的 mac 提供统一的开发环境。



# 安装和配置 Docker

下面的内容将介绍如何下载安装`Docker`，并且为`Docker`配置镜像

## 2.1 下载并安装 Docker

1. 访问[ Docker 官网](https://link.zhihu.com/?target=https%3A//hub.docker.com/) 了解和下载 `Docker` （下载地址：[Install Docker Desktop on Mac](https://docs.docker.com/desktop/install/mac-install/)）

> 如果你的 mac 是 apple silicon 的 芯片，那需要的是 arm  版本的 docker 

2. 安装成功后，在终端中输入 `docker --version`  命令查看 `Docker` 版本会得到下面类似信息：

```bash
> docker --version
Docker version 20.10.5, build 55c4c88
```

3. 验证 docker 的功能是否都正常：

如果 `docker version` 都正常的话，可以尝试运行一个 [Nginx 服务器](https://hub.docker.com/_/nginx/)：

输入 `docker run -d -p 80:80 --name webserver nginx` 命令

会看到如下内容：

```bash
➜  ~ docker run -d -p 80:80 --name webserver nginx 
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
33847f680f63: Pull complete 
dbb907d5159d: Pull complete 
8a268f30c42a: Pull complete 
b10cf527a02d: Pull complete 
c90b090c213b: Pull complete 
1f41b2f2bf94: Pull complete 
Digest: sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90
Status: Downloaded newer image for nginx:latest
39261d2d0f03071348332c34dd8fe705564e6291d958d1d17d2f99f7a2efebdb
```

服务运行后，可以访问 [http://localhost](http://localhost/)，如果看到了 "Welcome to nginx!"，就说明 Docker Desktop for Mac 安装成功了。

![install-mac-example-nginx](./img/install-mac-example-nginx.png)

要停止 Nginx 服务器并删除执行下面的命令：

```bash
docker stop webserver
docker rm webserver
```

命令运行结果如下所示：

```bash
➜  ~ docker stop webserver
webserver
➜  ~ docker rm webserver
webserver
➜  ~ 
```



## 2.2 配置 Docker镜像源（只对国内用户）

国内从 `Docker Hub` 拉取镜像有时会遇到困难，此时可以配置镜像加速器。`（国外用户不需要）`

国内很多云服务商都提供了国内加速器服务，例如：

- 阿里云加速器(点击管理控制台 -> 登录账号(淘宝账号) -> 右侧镜像中心 -> 镜像加速器 -> 复制地址)
- 网易云加速器 https://hub-mirror.c.163.com
- 百度云加速器 https://mirror.baidubce.com

由于镜像服务可能出现宕机，建议同时配置多个镜像。

> 国内各大云服务商（腾讯云、阿里云、百度云）均提供了 Docker 镜像加速服务，建议根据运行 Docker 的云平台选择对应的镜像加速服务。 

我们以 网易云 镜像服务 https://hub-mirror.c.163.com 为例进行介绍。

### Windows 10

TIPS：如果是在`win10`中，在`2004`版本之前，`docker`都是基于`Hyper-V`，`2004`版本之后默认使用 `WSL 2` 来运行。

> 如果你使用 windows 且还没有安装 WSL2，可以参考 [微软官方的教程](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10) 来配置 WSL2。记得要 WSL2 不是 WSL1

对于使用 `Windows 10` 的用户，在任务栏托盘 `Docker` 图标内右键菜单选择 `Settings`，打开配置窗口后在左侧导航菜单选择 `Docker Engine`，在右侧像下边一样编辑 `json` 文件，之后点击 `Apply & Restart` 保存后 `Docker` 就会重启并应用配置的镜像地址了。

```json
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```

> 注意，一定要保证该文件符合 `json` 规范，否则 `Docker` 将不能启动。

之后重新启动服务。

### macOS

对于使用 `macOS` 的用户，在任务栏点击 `Docker Desktop` 应用图标 -> `Perferences`，在左侧导航菜单选择 `Docker Engine`，在右侧像下边一样编辑 `json` 文件。修改完成之后，点击 `Apply & Restart` 按钮，`Docker` 就会重启并应用配置的镜像地址了。

```json
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```

> 注意，一定要保证该文件符合 `json` 规范，否则 `Docker` 将不能启动。

之后重新启动服务。

### 检查加速器是否生效

在终端执行 `docker info` 命令，如果从结果中看到了如下内容，说明配置成功。

```bash
Registry Mirrors:
 https://hub-mirror.c.163.com/
```



# 安装 homebrew

> homebrew 相当于 debian 的 apt 、arch 的 pacman、centos 的 yum

## 先安装 xcode 编译工具链

在终端执行下面的命令：

```shell
xcode-select --install
```

## 安装 brew 本体

> 如果已经安装则无视，具体可以参考 [brew 官方教程](https://brew.sh/index_zh-cn)

国外在终端执行命令安装 brew:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

如果是国内用户，可以会使用 gitee 的镜像：

```shell
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```



# 安装 Python 和 Pycharm



参考：`tutorial_pdf/安装python和pycharm` 这部分教程

关于 Python 解释器版本的选择：

令狐老师在视频中使用的是 Python3.6，我们可以直接安装最新的 Python3.10，因为 Python 是向下兼容的

> macbook apple Silicon (ARM) 支持 Python3.9+ 



# Docker 简介



docker 的工作流：



![](./img/docker001.png)



项目代码打包成一个 Docker 镜像，然后在根据这个镜像跑成一个容器



> 关于 Docker 的更多介绍以及使用教程可以参考：[Docker 从入门到实践](https://yeasy.gitbook.io/docker_practice/)





项目往往有很多依赖，比如需要 redis、mysql、hbase等等工具，同时现在流行微服务，服务本身就会被拆成多个子服务，和这个时候，使用 docker-compose 就可以帮我们一键批量管理多个容器了





![](./img/docker简介.png)





# 使用 docker-compose 来管理依赖

使用 docker 可以方便跑 redis、memcached 等等工具，但又因为这些工具多，一个一个手动管理就麻烦了。

借助 docker-compose 就可以方便的批管理，一键创建所有，一键开启所有，一键关闭所有

> 在本教程中项目的管理和工具是分开的，想和一起也还是可以的



