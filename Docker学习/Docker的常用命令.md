# Docker的常用命令

## 帮助命令

```shell
docker version     #显示docker的版本信息
docker info        #显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help  #帮助命令
```

帮助文档的地址：https://docs.docker.com/reference/

## 镜像命令

**docker images**   查看所有本地主机三的镜像

```shell
XX@linuxbox:~$ docker images
REPOSITORY                                   TAG       IMAGE ID       CREATED       SIZE
registry.hub.docker.com/lxk0301/jd_scripts   latest    ba92419ae695   3 weeks ago   154MB

#解释
REPOSITORY 镜像的仓库源
TAG        镜像的标签
IMAGE ID   镜像的id
CREATED    镜像的创建时间
SIZE       镜像的大小

#可选项
  -a, --all             # 列出所有的镜像
  -q, --quiet           # 只显示镜像的id
```

**docker search** 搜索镜像

```shell
XX@linuxbox:~$ docker search jd_scripts
NAME                          DESCRIPTION                         STARS     OFFICIAL   AUTOMATED
lxk0301/jd_scripts            暂无                                  311                  
akyakya/jd_scripts            京东小游戏&签到                            55                   
ohmypatrick/jd-base           自用 lxk0301/jd_scripts 套壳工具          15                   
thisispatrick/jd-base         自用 lxk0301/jd_scripts 套壳工具，尽可能简单…   15                   
junzhouliu/jd_scripts_gitee                                       2                    
aaron2397/jd_scripts                                              2    

# 可选项，通过收藏来过滤
--filter=STARS=300   # 搜索出来的镜像就是STARS大于300的
XX@linuxbox:~$ docker search jd_scripts --filter=STARS=300
NAME                 DESCRIPTION   STARS     OFFICIAL   AUTOMATED
lxk0301/jd_scripts   暂无            311                  
qb@linuxbox:~$ 

```

**docker pull**   下载镜像

```shell
# 下载镜像 docker pull 镜像名[:tag]
XX@linuxbox:~$ docker pull lxk0301/jd_scripts
Using default tag: latest  # 如果不写 tag，默认就是 latest
latest: Pulling from lxk0301/jd_scripts
......
Digest: sha256:201832c6499db818bbcbf2f5e0ea18d54b7042e79afcc06bc70c633326b715f1 # 签名
Status: Downloaded newer image for lxk0301/jd_scripts:latest
docker.io/lxk0301/jd_scripts:latest  # 真实地址
```

**docker rmi ** 删除镜像

```shell
docker rmi -f 镜像id  #强制删除指定的镜像
docker rmi -f 镜像id 镜像id 镜像id...  #强制删除多个指定的镜像
docker rmi $(docker images -aq)  #强制删除全部镜像
```



## 容器命令

说明：有了镜像才可以创建容器

```shell
docker pull lxk0301/jd_scripts
```

**新建容器并启动**

```shell
docker run [可选参数] image
# 参数说明
--name="Name"     容器名字，用来区分容器
-d                后台方式运行
-it               使用交互方式运行，进入容器查看内容
-p                指定容器端口 -p 8080:8080
  -p ip:主机端口:容器端口  （常用）
  -p 容器端口
  容器端口
  
-p                随机指定端口

# 测试，启动并进入容器
docker run -it jd_scripts /bin/sh
# 从容器中退回主机
exit
```

**列出所有运行的容器**

```shell
# docker ps 命令
    #列出当前正在运行的容器
-a  #列出当前正在运行的容器+带出历史运行过的容器
```

