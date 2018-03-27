### git的安装配置

#### 介绍

  Git 是__分布式__版本控制系统(distributed version control system)，最初由linux之父**Linus Benedict Torvalds**在2005年开发，是目前最流行的版本管理系统。

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
