# RPM (The RPM Package Manager) Linux 下广泛使用的软件包管理器。


    *RPM 软件包分为二进制包(Binary)、源代码包(Source) 和Delta包三种。源代码包以src.rpm作为后缀名*

### rpm包在打包过程中，会将文件临时安装到系统中，为了保证构建程序不破坏系统，要使用**普通用户**大包

### rpm打包工具
    
#### **rpmbuild**

  *安装rpmbuild* 
    
    $ yum install rpm-build 或者  yum install -y rpmdevtools

  *rpmbuild 依赖工具*

    $ yum install -y gcc gcc-c++ make

  *安装spec配置检查工具*

    $ yum install -y rpmlint

  *rpmbuild 常用参数*

    * --initdb: 初始化数据库?
    * --rebuilddb: 从已安装的包头文件，重建rpm数据库?
    * -ba: 创建二进制和源代码包
    * -bb: 创建二进制代码包
    * -bs: 创建源代码包
    * -bp: 执行到%prep结束
    * -bc: 执行到%build结束
    * -bi: 执行到%install结束
    * --short-circuit 可以跳过之前成功的阶段，节省时间

  *初始化打包环境, 在用户主目录下创建rpmbuild目录(BUILD、RPMS、SOURCES、SPECS、SRPMS)和.rpmmacros文件*

    $ rpmdev-setuptree

  *将要打包的源码和补丁放在SOURCES目录中*

  *进入SPECS目录，创建spec文件*

    $ rpmdev-newspec xxx.spec
    
  *检查spec配置文件*

    $ rpmlint xxx.spec

  *打包*

    $ rpmbuild -ba <specfile>

  *rpm软件包签名*

    在打包用户下，在~/.rpmmacros中添加
    %_signature gpg
    %_gpg_name willis

    签名
    rpm --addsign xx.xx.xx.rpm

##### spec 文件解析

  *自定义宏*
    
    %define <宏> <值>

    Name: 软件名，与spec文件名一致
    Version: 软件主版本号
    Release: 1%{?release}%{?dist}  发布编号，没打包一次值递增，主版本号发布后需重置该值
    Summary: 软件描述
    License: GPLv2  软件许可
    URL: 软件项目主页
    Source0: %{name}-%{version}.tar.gz 放置在SOURCES目录下的软件源码包名,可以指定多个Source1,...
    patch0: 补丁名，也可以多个
    buildroot: %_topdir/BUILDROOT   在install阶段的测试安装目录，方便写files
    BuildRequires: gcc,make 编译过程中需要的软件
    Requires: 安装软件包时所需要的依赖包列表
    %description 程序的详细描述，不超过80个字符
    
    %prep 准备阶段
        %setup -q  静默模式解压并进入解压后的目录，也常用：%autosetup -n %{name}

    %build 编译阶段
        make %{?_smp_mflags}  使用多核处理器并行编译

    %install 安装阶段
        rm -rf $RPM_BUILD_ROOT 删除之前的残留文件
        gmake install DESTDIR=$RPM_BUILD_ROOT 指定安装的虚拟目录

    %pre 安装前执行的脚本命令
        if [ $1 == 1 ];then  $1==1 代表的是第一次安装，2代表升级，0代表卸载   
            ...
        fi 

    %post 安装后执行的脚本命令
        
    %preun 卸载前执行的脚本命令
        if [ $1 == 0 ];then 
            ...
        fi 
    
    %postun 卸载后执行的脚本命令

    %clean
        rm -rf %{buildroot}  删除buildroot目录

    %files
        %defattr (-, root, root, 0755) 设定静默权限

    %changelog 变更日志，格式固定，生成用命令：rpmdev-bumpspec --comment=COMMENT --userstring=NAME+EMAIL_STRING <specfile>

#### **rpm_create**
#### **multipkg**
#### **fpm**
