### git的安装配置

#### 介绍

  Git 是**分布式**版本控制系统(distributed version control system)，最初由linux之父**Linus Benedict Torvalds**在2005年开发，是目前最流行的版本管理系统。

#### 安装(此处之介绍在mac下用brew安装)

  一般系统都会内置git，可通过`git --version`命令来查看是否已安装及安装版本

  brew 如果没有安装，先安装brew
    
    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

  如果已经安装brew，则更新
    
    $ brew update

  安装git
    
    $ brew install git

  将默认安装的git修改为刚安装的git版本
    
    $ brew link --force git  
    
  然后重新打开terminal

  更新git
    
    $ brew upgrade git

#### 配置

  查看当前用户名

    $ git config --global user.name

  设置用户名

    $ git config --global user.name "YOUR_USERNAME"

  设置邮箱

    $ git config --global user.email "example@example.com"

  以上配置是全局的，只需配置一次。下面介绍一下配置的三个层级
  项目层级，只对当前project有效，配置文件`.git/config`
  
    $ git config user.name "YOUR_USERNAME"

  用户层级，对当前用户所有项目有效，配置文件`~/.git/config`

    $ git config --global user.name "YOUR_USERNAME"

  系统层级，对所有用户的所有的项目有效，配置文件`/etc/gitconfig`

    $ git config --system user.name "YOUR_USERNAME"

  设置当前项目用户名，邮箱，进入当前项目目录
    
    $ git config user.name "YOUR_USERNAME" 
    $ git config user.email "YOUR_EMAIL"
    此时用git config --list 会发现有两个不同的用户名，邮箱，会优先用项目级别用户名，邮箱
    

  *为了确保你的提交呈现在你的贡献图（contribution graph)中，需要使用**GitHub验证**的邮件地址进行提交*

  列出git配置

    $ git config --global --list

#### 克隆项目

    $ git clone <版本库地址> <本地目录名>
  
  >远程克隆
  >> ssh 
  
    $ git clone username@host:/path/to/repository
  
  >> https

    $ git clone https:///path/to/repository

#### 我常用的配置信息

    alias.last=log -1
    alias.lg=log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen (%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --
    alias.br=branch
    alias.ci=commit
    alias.co=checkout
    alias.st=status
    color.ui=true
    url.https://github.com.insteadof=git://github.com
    user.name=muyuefei
    user.email=muyuefei158@gmail.com
    merge.tool=vimdiff

![](https://sdtimes.com/wp-content/uploads/2014/08/0826.sdt-git-21.jpg)
