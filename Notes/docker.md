# **Docker**

***

### **docker 的核心组件**
    * Docker客户端和服务器，即Docker引擎
    * Docker 镜像
    * Registry
    * Docker 容器

### **docker 的目标/优势**
1. 提供一个简单、轻量的建模方式
2. 职责的逻辑分离
3. 快速、高效的开发生命周期
4. 鼓励使用面向服务的架构
    * 推荐单个容器只运行一个应用程序或进程

### **docker 的注意项**

### **安装docker的先决条件**
    * 64位的CPU架构，不支持32位
    * Linux3.8以上版本内核
    * 内核必须支持一种适合的存储驱动
    * 内核必须支持并开启cgroup和命名空间namespace功能

### **docker 安装脚本**
    
    $ curl https://get.docker.com/ | sudo sh

### **常用命令**

1. `docker run -it -v <local dir>:<container dir> -p <local port>:<container port> --log-driver --restart=always --name <container name> -d  xxx bash`

    * "run": 启动容器
    * "-i":  交互
    * "-t":  终端
    * "-d":  后台执行
    * "-v":  指定容器挂在宿主机目录
        * 可以在<container port>后加上'rw'或者'ro'指定目录的读写状态, 如" -v xxx:/root/dir:ro"，代表只能读
    * "-p":  指定容器映射宿主机端口, 如果是“-P”, 表示dockerfile中expose的所有容器端口都通过宿主机公开
    * "--log-driver": 指定日志驱动，默认json-file
    * "--name": 容器名称
    * "--restart": 容器在什么条件下重启
        * always: 无论什么情况下退出，都重启
        * on-failure:n: 只有当退出码非0时，才会重启, 最多n次
    * "xxx": 容器镜像
    * "bash":shell交互方式

2. `docker images / docker image ls` 
    列出镜像
3. `docker ps`
    列出所有活跃容器
4. `docker ps -a`
    列出所有容器
5. `docker start/stop/restart xxx`
    启动/停止/重启  容器
6. `docker pull/push xxx registry`
    从/向指定仓库拉取/推送 镜像, 默认docker hub

7. `docker system df`
    列出docker所占用空间大小
8. `docker images -f dangling=true`
    "-f" 是"--filter" 过滤器, 列出所有虚悬镜像--> 仓库名、标签均为none的镜像
9. `docker images prune`
    删除所有的虚悬镜像
10. `docker images --format "{{.ID}}"` 
    "--format" docker 模版语言格式化
11. `docker image rm image1 image2`    
    删除镜像
12. `docker images --digests`
    列出镜像摘要
13. `docker commit --author "xx" --message "" 镜像名 镜像registry名:tag`
    提交修改到镜像
14. `docker diff <container>`
    查看容器做的修改
15. `docker history 镜像registry名:tag`
    查看某个镜像的修改历史
16. `docker attach <container>`
    重新附着到容器会话上，退出则容器也stop
17. `docker logs <container>`
    查看容器日志
18. `docker logs --tail 0 -f -t <container>`  
    实时追踪容器最新日志, 并加上时间戳
19. `docker top <container>`  
    查看容器进程
20. `docker stats <container>`  
    查看容器cpu,mem等统计信息
21. `docker exec <container> command`
    在容器中执行命令
22. `docker ps -n x`
    查看最后的x个容器，包含stop的
23. `docker inspect --format '{{ .Name }} {{. State.Running}}' <container>
    对容器进行详细配置检查，--format 标志显示结果，通过{{.attribute}}来调用属性信息
24. `docker build --no-cache -t=<new image name>  <docker file path>`
    忽略Dockerfile的构建缓存，docker file path 可以是git版本库中的dockerfile地址
25. `docker port <container> <port>`
    查看容器的端口映射情况
    

### 注意点
1. docker rmi 镜像，当有多个别的标签指向同一个镜像时，有可能只会删除镜像标签，而并没有真正删除镜像。
2. docker 容器是依赖镜像为基础的，当镜像有容器存在（无论是否活跃），则无法删除。

3. docker 命令联合使用，例：`docker rmi $(docker images -f since=mongo3.2)`

4. 不要用`docker commit` 来定制镜像，要定制镜像用Dockerfile.

### Dockerfile
*docker 语法分两部分： 注释和命令+参数*
1. "FROM" --> 指定基础镜像

2. "RUN"  --> 执行命令行命令
    * shell 格式：RUN <命令>
    * exec  形式: RUN ["可执行文件", "参数1", "参数2"]

3. "COPY" --> 跟"ADD"基本一样, 不支持资源地址下载与解压缩

4. "MAINTAINER" --> 维护者信息

5. "CMD" --> 容器启动时执行命令
    * CMD ["executable", "param1", "param2"]使用exec执行，推荐使用
    * CMD command param1 param2 在/bin/sh 上执行
    * CMD ["param1", "param2"]提供给entrypoint做默认参数
    * *每个容器只能执行一条CMD命令，多个CMD命令时，只执行最后一条*

6. "USER" --> 指定运行容器时的用户名或UID

7. "VOLUME" --> 用于容器共享宿主机文件目录

8. "WORKDIR" --> 用于设置CMD指明的命令的运行目录

9. "ENV" --> 指定一个环境变量，后续会被RUN指令使用, 如：ENV foo /bar，可以用${foo}调用
    * "REFRESHED_AT" --> 该环境变量表明该镜像模版的最后更新时间

10. "ADD" --> 从源系统的文件系统上复制文件到目标容器的文件系统.如果源是一个资源地址，那么该资源会被下载并复制到容器中，如果是压缩资源，也会做解压处理.

11. "EXPOSE" --> 指定在docker允许时指定的端口进行转发, 及端口映射

12. "ENTRYPOINT" --> 配置容器启动后执行的命令，不会被docker run 提供的参数覆盖
    * ENTRYPOINT ["executable", "param1", "param2"]
    * ENTRYPOINT command prama1 prama2 在shell中执行
    * *每个dockerfile只能有一个ENTRYPOINT, 即使有多个也会只执行最后一个*

13. "ONBUILD" --> 指定的命令在构建时并不执行，而是在它的子镜像中执行, 即：当我们在dockerfile中添加这条指令，不会对当前构建镜像起作用，但当我们再用一个新的基于这个镜像的dockerfile构建镜像时就会执行指令。

14. "STOPSIGNAL" --> 指定stop容器的信号

15. "HEALTHCHECK" --> 容器进程健康心跳监测, 如："HEALTHCHECK --interval=5m --timeout=3s --start-period=3s --retries=3 CMD curl -f http://localhost/ || exit 1
    * --interval=DURATION(default:30s)
    * --timeout=DURATION(default:30s)
    * --start-period=DURATION(default: 0s) 启动时间，在启动时间内健康检测次数不纳入retries次数
    * --retries=N (default:3) 重试N次后才会视为unhealth

16. "SHELL" --> 指定默认shell， 如:'SHELL ["powershell", "-command"]' 覆盖默认的shell

17. "LABEL" --> 用于为镜像添加元数据，以键值对形式指定，指定后可以通过"docker inspect"  查看

18. "ARG" --> 指定传递给构建运行时的变量，如"ARG build_user=xxx", 可以在构建时用"docker build --build_user=xx" 指定xx并覆盖xxx


### 构建docker内部通信


### 构建Jenkins和Docker服务器

### Docker Api
