# 集成sso-client demo


集成步骤<br />

####1. sso-client-provider项目打成jar包(子系统不用操作)
- 进入sso-client-provider项目下，先清空target：mvn clean
- 打包：mvn package -DskipTests=true
- 生成sso-client-jar-with-dependencies.jar

####2. 其他子系统集成(子系统的操作)
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
#系统编码(与认证中心一致)
sys.config.mySysCode=sys-client01
#MD5签名秘钥(与认证中心-平台详情-添加的秘钥一致)
sys.config.ssoAuthSecret=1234567890

#认证中心登录地址
sys.config.ssoAuthLoginUrl=http://172.16.18.71:8010/login
#当前客户端web地址
sys.config.clientWebUrl=http://localhost:8801
#本系统退出登录url
sys.config.myLoginOutUrl=http://localhost:8801/logOutBySsoAuth
#认证中心开放接口地址
sys.config.ssoAuthGetWayUrl=http://172.16.18.71:9901/api/open/gateway
```
- 主启动类中添加包扫描注解
```
@ComponentScan(basePackages = {"com.example.sso.***"})
```

