## 初始化项目


先保证自己电脑有一个 python3.9 或者 python3.10


下面以 3.10 为例子


如果你是国内用户，先找终端输入下面的代码。作用是全局替换 pypi 清华镜像源

```shell
pip3.10 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```




安装一个 pipenv，来创建和管理我们的 python 虚拟环境

```shell
pip3.10 install pipenv
```

> [关于 python 虚拟环境管理器的选择](https://segmentfault.com/a/1190000042541342)



我这里用 vscode 做演示

![image-20220924174029752](./img/image-20220924174029752.png)

> 我自己建立的项目，没有叫做 django-twitter，而是叫做 twitter


### 1. 创建项目

接下来我们要开始从零开始创建一个项目了，在此之前我们需要创建一个新的分支 `2-initial-django` ，在终端执行 

```shell
git checkout -b 2-initial-django
```


创建虚拟环境：

```shell
╰─➤  pipenv install --python=python3.10
Creating a virtualenv for this project...
Pipfile: /Users/ponponon/Desktop/code/jiuzhang/twitter/Pipfile
Using /Library/Frameworks/Python.framework/Versions/3.10/bin/python3.10 (3.10.7) to create virtualenv...
⠼ Creating virtual environment...created virtual environment CPython3.10.7.final.0-64 in 176ms
  creator CPython3Posix(dest=/Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/ponponon/Library/Application Support/virtualenv)
    added seed packages: pip==22.2.2, setuptools==65.3.0, wheel==0.37.1
  activators BashActivator,CShellActivator,FishActivator,NushellActivator,PowerShellActivator,PythonActivator

✔ Successfully created virtual environment! 
Virtualenv location: /Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW
Creating a Pipfile for this project...
Pipfile.lock not found, creating...
Locking [dev-packages] dependencies...
Locking [packages] dependencies...
Updated Pipfile.lock (e4eef2)!
Installing dependencies from Pipfile.lock (e4eef2)...
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

> `pipenv install --python=python3.10` 如果不加后面的 `--python=python3.10` 会自动选择按 env 发现的第一个 python 创建虚拟环境。
>
> 我们明确指定一下需要 python3.10 。
>
> 需要注意，这个 python3.10 在你电脑上必须已经存在了，因为创建虚拟环境本质是建立了一个软连接，你没有 python3.10，这个软链接就无从谈起。

这个时候，我们在资源管理器中就会看到多了两个文件

![image-20220924174308440](./img/image-20220924174308440.png)



- Pipfile 
- Pipfile.lock 

用来管理虚拟环境和第三方包的

> [关于 python 虚拟环境管理器的选择](https://segmentfault.com/a/1190000042541342)



> 插入一个 pipenv 简易教程(更多内容看官方文档：[pipenv doc](https://pipenv.pypa.io/en/latest/))：
>
> 创建虚拟环境: `pipenv install`
>
> 激活虚拟环境: `pipenv shell`(看到有 project name 作为命令提示符前缀了，就说明虚拟环境激活ok了)
>
> 删除虚拟环境：`pipenv shell`

接下来在终端输入 `pipenv shell` 激活虚拟环境

```shell
╰─➤  pipenv shell                      
Launching subshell in virtual environment...
 . /Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW/bin/activate
╭─ponponon@MBP13ARM ~/Desktop/code/jiuzhang/twitter  ‹main*› 
╰─➤   . /Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW/bin/activate
(twitter) ╭─ponponon@MBP13ARM ~/Desktop/code/jiuzhang/twitter  ‹main*› 
```

可以看到，前面多了一个 twitter 的提示符，这表明已经在 twitter 这个虚拟环境中了

```shell
╰─➤  where python
/Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW/bin/python
(twitter) ╭─ponponon@MBP13ARM ~/Desktop/code/jiuzhang/twitter  ‹main*› 
╰─➤  
```

这个时候，我输入 where python ，可以看到这个 python 的路径

```shell
╰─➤  ll /Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW/bin/python         
   inode Permissions Links Size Blocks User     Group Date Modified Name
14000043 lrwxr-xr-x      1   65      0 ponponon staff 24 Sep 17:41  /Users/ponponon/.local/share/virtualenvs/twitter-Xx4DzOMW/bin/python -> /Library/Frameworks/Python.framework/Versions/3.10/bin/python3.10
```

而这个路径其实是我们自己安装的 python3.10 的一个软连接。



![image-20220924175424650](./img/image-20220924175424650.png)

需要两个文件：

创建一个 `requirements-prd.txt`, 内容如下👇

```txt
Django==3.1.3
pymysql
```

创建一个 `requirements-dev.txt`, 内容如下👇

```txt
mycli
ipython
autopep8
psutil
```

通过下面两个命令安装他们

```shell
pip install -r requirements-prd.txt 
pip install -r requirements-dev.txt 
```



在当前目录下创建一个名为 `twitter` 的项目：

> 如果你的仓库名，叫 django-twiiter ，那这里就叫做 django-twiiter 吧

```shell
django-admin startproject twitter .
```

>不要忘记后面有一个 `.` 点哦。



![image-20220924182023022](./img/image-20220924182023022.png)

可以看到多了好多文件

好了，我们把这个项目跑起来吧！







# 直接跑

直接在终端输入 `python manage.py runserver 0.0.0.0:8888` ，然后在浏览器输入 `127.0.0.1:8888` 就能看到了  

```shell
╰─➤  python manage.py runserver 0.0.0.0:8888                                                                                                           130 ↵
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
September 24, 2022 - 10:47:34
Django version 3.1.3, using settings 'twitter.settings'
Starting development server at http://0.0.0.0:8888/
Quit the server with CONTROL-C.
```



看到这个界面就是 ok 了

![image-20220924184835799](./img/image-20220924184835799.png)





# 使用 docker 跑



因为我们后续需要数据库之类的东西，让我们想用 docker 把 mysql、redis 这些中间件跑起来吧！




------------------



先在你的项目根目录(不是系统根目录哦)，新建下面三个文件吧

- `Makefile` 文件，管理 docker-compose 的工具（docker-compose 管理多个容器，再用 make 管理docker-compose 多次套娃）
- `docker-compose-tools.yaml` 文件
- `redis.conf`





`Makefile` 文件

```makefile
NAME = jiuzhang/twitter
# jiuzhang/twitter 就是镜像名，可以改成你自己的，格式： {随意，一般用公司名或者个人名}/{项目名}


.PHONY: build up stop logs

build:  docker-build
up: docker-compose-up
stop: docker-compose-stop
logs: docker-compose-logs

docker-build:
	docker build -t "${NAME}" .

docker-compose-up:
	docker-compose up -d

docker-compose-stop:
	docker-compose stop

docker-compose-logs:
	docker-compose logs --tail=100 -f
```

> 为什么使用 Makefile 来管理 docker-compose 可参考：[使用 makefile 管理 docker-compose ](https://segmentfault.com/a/1190000041379546)

先准备一个`docker-compose-tools.yaml` 文件，在这个文件中，准备了 mysql 、redis、memcahed 之后需要 hbase 也可以加进来

```yaml
# docker-compose up -f docker-compose-tools.yaml

version: "3"
services:
  mysql8:
    platform: linux/amd64 # 不加这行会报：ERROR: no matching manifest for linux/arm64/v8 in the manifest list entries
    container_name: mysql8
    image: mysql:8.0 # 镜像会从 docker hub 中拉取。地址: https://hub.docker.com/_/mysql?
    ports:
      - "3306:3306" # 冒号左边的宿主机的端口，右边的是容器的端口
    restart: always # 如果容器停止，请始终重新启动容器。  如果是手动停止的，只有在 Docker daemon 重启或者容器本身手动重启时才会重启。https://docs.docker.com/config/containers/start-containers-automatically/
    volumes:
      - /usr/local/mysql/data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: 123456 # root 账号的密码，记得把 Django settings.py 里面 mysql 配置项的密码和这个对应起来

  redis:
    container_name: redis
    image: redis:latest
    ports:
      - "6379:6379"
    volumes:
      - /usr/local/redis/data:/data # /usr/local/redis/data 是你宿主机的路径；/data 是容器内的路径，容器内的 redis 会把需要持久化的数据都保存到 /data 目录下
      - ./redis.conf:/etc/redis/redis.conf # redis.conf 这个文件已经准备好了，可以放到这个路径，也可以自己修改，比如放到项目路径中
    restart: always
    command: redis-server /etc/redis/redis.conf

  memcahed:
    container_name: memcahed
    image: memcached:latest
    restart: always
    ports:
      - "11211:11211"

# QA:
# Q: 为什么 redis 使用了 volumes，而 mysql 没有使用 volumes
# A：挂了 volumes 之后，容器的 rm 之后重新 run 一个，数据也不会丢，想要这个特性就可以给 mysql 也挂上，因为这个项目是学习用途，所以不加也没事
# 生产环境中，mysql 一般也不会容器化部署，redis 倒是容器化部署挺多的，因为 mysql 要求的可靠性比 redis 高一些。

```

再来一个 `redis.conf`文件，

```yaml
# 这个文件的地址，和你的 docker-compose.yaml 中的 /usr/local/redis/redis.conf:/etc/redis/redis.conf 冒号左边的要对应起来
# redis 支持两者持久化机制：RDB&AOF
# https://juejin.cn/post/6844903716290576392

appendonly yes
#default: 持久化文件
appendfilename "appendonly.aof"
#default: 每秒同步一次
appendfsync everysec

port 6379
# 绑定端口,不指定外网可能连不上服务器
bind 0.0.0.0
```

> 配置这个文件主要是为了 `bind 0.0.0.0` 这行，不加这个的话，就无法访问到 redis 了，其他的 aof 持久化等等都不是必须的

在宿主机终端输入 `docker-compose -f docker-compose-tools.yaml up ` 命令

结果如下：

```shell
─➤  docker-compose -f docker-compose-tools.yaml up                                                                                        
Pulling mysql8 (mysql:8.0)...
8.0: Pulling from library/mysql
c1ad9731b2c7: Pull complete
54f6eb0ee84d: Pull complete
cffcf8691bc5: Pull complete
89a783b5ac8a: Pull complete
6a8393c7be5f: Pull complete
af768d0b181e: Pull complete
810d6aaaf54a: Pull complete
2e014a8ae4c9: Pull complete
a821425a3341: Pull complete
3a10c2652132: Pull complete
4419638feac4: Pull complete
681aeed97dfe: Pull complete
Digest: sha256:548da4c67fd8a71908f17c308b8ddb098acf5191d3d7694e56801c6a8b2072cc
Status: Downloaded newer image for mysql:8.0
Pulling memcahed (memcached:latest)...
latest: Pulling from library/memcached
dc1f00a5d701: Pull complete
f92712d311c9: Pull complete
31a9b9dc2f1c: Pull complete
eedb3694eb80: Pull complete
e9956e0fb928: Pull complete
0ca725a9ac6a: Pull complete
Digest: sha256:54518a05dfeb26ad8994e32ac50f47db44bc9ec1a8713fa7464c3b88bfa29d91
Status: Downloaded newer image for memcached:latest
Creating redis    ... done
Creating mysql8   ... done
Creating memcahed ... done
Attaching to mysql8, memcahed, redis
```

> 现在是前台运行，也可以使用  `docker-compose -f docker-compose-tools.yaml up -d` 命令，这样就会跑在后端，关闭终端也不会让 redis、mysql 退出



好的，我们可以验证一下是不是真的跑起来了

先安装一些小工具

```shell
brew install iproute2mac
```

使用 `ip a` 命令查看你的电脑的ip 地址

一般就看 en0 对应的 ip 地址，比如下面的结果就是 `192.168.31.100`

```shell
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
        ether 3c:06:30:2c:de:bd
        inet6 fe80::140c:c42f:4e76:fd65/64 secured scopeid 0xb
        inet 192.168.31.100/24 brd 192.168.31.255 en0
```



再安装 mycli，这是一个 mysql 第三方 client

> 为什么用 mycli，而不是 mysql 官方的 client 呢？因为单独安装官方的 mysql client 麻烦，而且也不好用。mycli 是 python 写的第三方客户端，带有：
> - 命令补全
> - 智能提示
> - 色彩高亮
> - 高危风险提示
> 等等功能, 是非常优秀的替代品

```shell
brew install mycli
```

使用 mycli 连接到 docker 中的 mysql

```shell
mycli -u root -p123456 -h xxx.xxx.xxx.xxx 
```

> xxx.xxx.xxx.xxx 就是你的私网 ip 地址，不是 127.0.0.1 哦，因为容器的 network 和宿主机是隔离的

输出如下：

```shell
─➤  mycli -u root -p123456 -h 192.168.31.100
MySQL 
mycli 1.25.0
Home: http://mycli.net
Bug tracker: https://github.com/dbcli/mycli/issues
Thanks to the contributor - Angelo Lupo
MySQL root@192.168.31.100:(none)>
```

> 在这里你可以手动创建 twitter 项目用到的 database



再安装 iredis，这是一个 redis 第三方 client

```shell
brew install iredis
```

使用 `iredis -h xxx.xxx.xxx.xxx` 连接到容器中的 redis 

输出如下：

```shell
─➤  iredis -h 192.168.31.100              
iredis  1.11.0 (Python 3.10.3)
redis-server  6.2.5 
Home:   https://iredis.io
Issues: https://iredis.io/issues
192.168.31.100:6379>
```

> 这次可以在 mycli 的 shell 中，输入 `create database twitter;` 先把数据库创建了

好了！依赖的工具就准备好了，下面看看项目本身吧！



# 使用 `docker-compose` 跑项目

`docker-compose.yaml`

```yaml
version: "3"
services:
  twitter:
    container_name: twitter
    image: jiuzhang/twitter
    ports:
      - "8000:8000" # 这里的端口改为和 python manage.py runserver 0.0.0.0:8000  一样的端口才行
    command: python manage.py runserver 0.0.0.0:8000
```

`Dockerfile` 文件

```dockerfile
FROM python:3.10-buster
RUN /usr/local/bin/python -m pip install --upgrade pip -i https://mirrors.aliyun.com/pypi/simple
RUN mkdir /code
WORKDIR /code
COPY requirements-prd.txt /code/
RUN pip install -i https://mirrors.aliyun.com/pypi/simple -r requirements-prd.txt
COPY . /code/
```


第一步构建镜像：`make build`

第二步运行镜像：`make up`

第三步查看镜像的日志：`make logs`



> 因为我们使用 make up 运行镜像的时候，其实是跑了 docker-compose up -d 命令， -d 参数表示后台运行（d就是detach的缩写，具体可以参考官方文档：[docker-compose up command](https://docs.docker.com/compose/reference/up/)）,所以我们是看不出程序的输出。此时 Docker 会默默的把程序的标准输出保存到一个 json 文件中，我们需要查看标准输出的话，并不需要只看这个 json 文件，而是可以使用 `docker-compose logs --tail=100 -f` 命令，但是这个命令太长了，使用 make logs 简化之

需要关闭程序，可以使用 `make stop`

每次代码有改动，都要需要重复上面三个步骤

也可以一行命令：`make build && make && make logs`



在浏览器地址栏输入 `127.0.0.1:8000` 就可以看到熟悉的界面了

![](./img/image-20220924184835799.png)

> 运行的时候，报错无法连接到数据库，去修改一下 twitter 项目下面的 settings.py 这个文件，找到 database 的 HOST 选项，把 HOST 改成你的私网 ip 地址