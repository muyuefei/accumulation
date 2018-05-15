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
13. `docker commit --author "xx" --message ""` 
    镜像名 镜像registry名:tag\n
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

