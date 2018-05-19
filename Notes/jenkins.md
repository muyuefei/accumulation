# Jenkins 知识整理
***

## Jenkins 安装
1. mac 
    `brew install jenkins`

## 忘记密码
1. 删除Jenkins目录下config.xml文件中下面代码，并保存文件。
```
    <useSecurity>true</useSecurity>  
    <authorizationStrategy class="hudson.security.FullControlOnceLoggedInAuthorizationStrategy">  
    <denyAnonymousReadAccess>true</denyAnonymousReadAccess>  
    </authorizationStrategy>  
    <securityRealm class="hudson.security.HudsonPrivateSecurityRealm">  
    <disableSignup>true</disableSignup>  
    <enableCaptcha>false</enableCaptcha>  
    </securityRealm>  
```

2. 重新加载配置文件 http://jenkins-server/reload

3. 进入首页>“系统管理”>“Configure Global Security”；

4. 勾选“启用安全”；

5. 点选“Jenkins专有用户数据库”，并点击“保存”；

