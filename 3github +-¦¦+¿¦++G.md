


先去 github , 创建自己的项目





### 配置公钥（可选）

> 如果你是第一次使用 git ，以前没有在该电脑上添加过公钥，那这步是必须的。

如果你在使用使用Git 克隆项目的时候遇到下面的问题，就需要配置以下公钥了。

```bash
git clone git@github.com:jiuzhangsuanfa/twitter-term-1.git
Cloning into 'twitter-term-1'...
The authenticity of host 'github.com (192.30.255.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,192.30.255.112' (RSA) to the list of known hosts.
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

或者这样也需要配置公钥，跟着下面的内容配置公钥就好了。

![image-20210519100227745](./img/0519-1.png)



**添加公钥的方法**

- 步骤一：在终端运行下面的命令，把邮箱换成自己的

  ```bash
  ssh-keygen -t rsa -C "email@email.com"
  ```
> 过程中只需要一路回车，不需要输入任何内容，默认会在~/.ssh路径下生成`id_rsa` 和`id_rsa.pub`文件。`id_rsa.pub`就是我们需要的。


  ![image.png](./img/100.png)

- 步骤二：查看 `~/.ssh`路径下的`id_rsa.pub`文件,并复制文件内容

  ![image.png](./img/101.png)

  > 生成的`id_rsa.pub`一般在`~/.ssh/`目录下。
  >
  > 注意：需要把从 **ssh-rsa**开始到**邮箱**的所有内容都复制

- 步骤三：打开自己的Github主页，选择设置

![image.png](./img/103.png)

- 步骤四：选择左侧的`SSH and GPG keys`，在选择`New SSH key`

![image.png](./img/104.png)

- 步骤五：把刚刚那个公钥复制到这里面就好了，title随便填，无所谓。点击`Add SSH key`保存。

![image.png](./img/105.png)

> 注意：因为生成的公钥是来自我们的宿主机，可以通过宿主机的git程序clone、pull代码
>
> 但是如果想要通过虚拟机来clone、pull、push代码的话，还需要让虚拟机也生成公钥，并添加到Github中。
>
> 因为虽然宿主机和虚拟机虽然都运行在同一台电脑上，但是是物理上是隔绝的，都有各自的git程序和密钥作用范围。
>
> 但是因为在.git 里面会记录一些和主机相关的信息，因为是共享文件夹，所以再在虚拟机中执行git指令的时候，有些信息会对不上就会报错，所以尽量在宿主机机器上操作吧！


# 创建代码仓库

首先我们打开我们的 github 页面，点击左上角的 + ，再点击 New repository 按钮创建一个新的仓库。

![](./img/52.png)

接下来会让你填写一些信息，比如我们代码仓库的名字 django-twitter，然后添加一个 `README.md` 文件.

![](./img/53.png)

填写完相关信息后，点击 Create repository 按钮，我们就创建了一个代码仓库。

![](./img/54.png)

> 注意选SSH，而不是左边的HTTPS 

### 4.克隆代码仓库

然后我们可以复制上图红框的部分，使用 `git clone` 命令将代码仓库复制到本地电脑的合适位置：

```shell
git clone git@github.com:yourname/django-twitter.git
```

如果 clone 成功，可以看到如下图所示提示，下图的操作我们是在宿主机的 Git Bash 上进行操作。

![](./img/55.png)

此时我们本地的目录结构大致为：

```shell
django-twitter
├── .git 
├── .gitignore
└── README.md
```

> 这里 `.git` 是一个隐藏文件夹，如果你在文件管理器中看不见这个文件夹，需要打开文件管理器的`查看隐藏文件`选项。
>
> 接下来的项目开发都是在自己的仓库进行的。






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










### 1. 创建项目

接下来我们要开始从零开始创建一个项目了，在此之前我们需要创建一个新的分支 `2-initial-django` ，在终端执行 

```shell
git checkout -b 2-initial-django
```


创建虚拟环境：

```shell
pipenv iinstall --python=python3.10
```




