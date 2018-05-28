# YUM(Yellow dog Updater, Modified), 一个基于RPM包管理的字符前端软件包管理器。可以一次性解决依赖关系。

***

### 创建私有yum仓库
  *创建yum仓库目录xxx/yum/xxx/x86_64*
   
  *进入yum仓库目录*

  *将rpm 包放在此目录下*

  *安装createrepo*

    $ yum -y install createrepo

  *初始化repodata索引文件*

    $ createrepo -pdo yum仓库目录 yum 仓库目录

  *用web服务器代理访问*
    * apache
    * nginx
    * python -m SimpleHTTPServer 80 & >/dev/null &

### yum 常用命令
  *只下载不安装*
    
    $ yumdownloader xxx
  
  *清除缓存*
    
    $ yum clean all
 
  *生成缓存*
    
    $ yum makecache
  
  *查找rpm包*
    
    $ yum search <keyword>
  
  *列出所有可更新的包*
  
    $ yum check-update

  *更新所有软件*
    
    $ yum update
  
  *更新指定软件*
  
    $ yum update xxx

  *列出所有可安装的软件*

    $ yum list

  *删除/卸载软件*

    $ yum remove xxx
