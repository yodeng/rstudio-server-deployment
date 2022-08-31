### Rstudio-Server

网页版多用户`Rstudio`使用部署，需使用`root`用户部署。

#### 依赖

+ linux64 @root
+ centos 7

#### 安装

```
yum -y install R
wget https://download2.rstudio.org/server/centos7/x86_64/rstudio-server-rhel-2022.07.1-554-x86_64.rpm
yum install rstudio-server-rhel-2022.07.1-554-x86_64.rpm
```

+ 安装完成后使用`rstudio-server version`，提示版本信息表示安装成功

#### 配置

`Rstudio-Server`默认端口`8787`，主要配置文件和配置项有以下：

`/etc/rstudio/rserver.conf`和`/etc/rstudio/rsession.conf`两个配置文件

```
# /etc/rstudio/rserver.conf
www-port=8787                                                ## 指定使用端口,Rstudio-Server默认使用8787端口
rsession-which-r=/home/dengyong/soft/miniconda3/bin/R        ## 指定默认R版本路径，默认root用户$(which R)路径
rsession-ld-library-path=/home/dengyong/soft/miniconda3/lib  ## 指定R使用的其他库
rsession-memory-limit-mb=4000                                ## 限制Rstudio-Server总内存
rsession-process-limit=100                                   ## 限制Rstudio-Server总进程数

## /etc/rstudio/rsession.conf
session-timeout-minutes=30                                   ## 网页Rstudio-Server会话连接超时时间
r-libs-user=/home/dengyong/R/packages                        ## 更改Rstudio-Server安装的R包默认路径
r-cran-repos=https://mirrors.tuna.tsinghua.edu.cn/CRAN/      ## Rstudio-Server安装R包镜像地址

```

#### 服务管理

`rstudio-server {start|status|restart|stop}`

#### 网页登录

网页打开`http://${IP}:${www-port}/`即可出现登录页面，输入普通用户账户和密码即可完成登录，`rstudio-server`禁止使用`root`登录。

#### 参考

[RStudio-Server](https://support.rstudio.com/hc/en-us/sections/200150693-RStudio-Workbench-RStudio-Server)

