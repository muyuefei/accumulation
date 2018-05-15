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
    

