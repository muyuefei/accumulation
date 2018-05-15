# **Docker**

***

### **常用命令**

1. `docker run -it xxx bash`
    "run": 启动容器
    "-i":  交互
    "-t":  终端
    "xxx": 容器镜像
    "bash":shell交互方式

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
14. `docker diff Container`
    查看容器做的修改
15. `docker history 镜像registry名:tag`
    查看某个镜像的修改历史
### 注意点
1. docker rmi 镜像，当有多个别的标签指向同一个镜像时，有可能只会删除镜像标签，而并没有真正删除镜像。
2. docker 容器是依赖镜像为基础的，当镜像有容器存在（无论是否活跃），则无法删除。

3. docker 命令联合使用，例：`docker rmi $(docker images -f since=mongo3.2)`

4. 不要用`docker commit` 来定制镜像，要定制镜像用Dockerfile.

### Dockerfile
*docker 语法分两部分： 注释和命令+参数*
1. "FROM" --> 指定基础镜像
2. "RUN"  --> 执行命令行命令
    *shell 格式：RUN <命令>
    *exec  形式: RUN ["可执行文件", "参数1", "参数2"]
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
9. "ENV" --> 指定一个环境变量，后续会被RUN指令使用
10. "ADD" --> 从源系统的文件系统上复制文件到目标容器的文件系统.如果源是一个资源地址，那么该资源会被下载并复制到容器中，如果是压缩资源，也会做解压处理.
11. "EXPOSE" --> 指定在docker允许时指定的端口进行转发, 及端口映射
12. "ENTRYPOINT" --> 配置容器启动后执行的命令，不会被docker run 提供的参数覆盖
    * ENTRYPOINT ["executable", "param1", "param2"]
    * ENTRYPOINT command prama1 prama2 在shell中执行
    * *每个dockerfile只能有一个ENTRYPOINT, 即使有多个也会只执行最后一个*
13. "ONBUILD" --> 指定的命令在构建时并不执行，而是在它的子镜像中执行, 即：当我们在dockerfile中添加这条指令，不会对当前构建镜像起作用，但当我们再用一个新的基于这个镜像的dockerfile构建镜像时就会执行指令。
