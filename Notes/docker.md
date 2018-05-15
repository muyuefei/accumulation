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
    

