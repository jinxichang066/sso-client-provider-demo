# 集成sso-client demo

集成步骤<br />

####子系统集成
- 将sso-client-jar-with-dependencies.jar引用项目中。以maven为例，有两种方式：  
######1.第一种方式是通过maven将本地jar安装到本地仓库中。  
######2.第二种方式则是将本地jar保存至项目的lib中，需要在项目的根目录中添加一个lib，将jar拷贝至lib中。本示例采用第二种方式,POM添加： 
```
<dependency>
            <groupId>com.example</groupId>
            <artifactId>sso-sys-client</artifactId>
            <version>1.0-SNAPSHOT</version>
            <scope>system</scope>
            <systemPath>${pom.basedir}/lib/sso-client-jar-with-dependencies.jar</systemPath>
</dependency>
```
- application配置文件配置  
```
#系统编码(认证中心提供)
sys.config.mySysCode=sys-client-zhijian
#MD5签名秘钥(认证中心提供)
sys.config.ssoAuthSecret=1234567890

#认证中心登录地址(认证中心提供)
sys.config.ssoAuthLoginUrl=http://172.16.18.71:8010/login
#当前客户端web地址(即当前应用的主页url)
sys.config.clientWebUrl=http://www.sso.test.com:8801
#本系统退出登录url(即当前应用的ip:port/应用上下文/logOutBySsoAuth，本样例没有配置上下文所以省略)
sys.config.myLoginOutUrl=http://www.sso.test.com:8801/logOutBySsoAuth
#认证中心开放接口地址(认证中心提供)
sys.config.ssoAuthGetWayUrl=http://172.16.18.71:9901/api/open/gateway
```
- 主启动类中添加包扫描注解
```
@ComponentScan(basePackages = {"com.example.sso.***"})
```

