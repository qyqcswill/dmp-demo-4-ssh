## DMP-demo-4-ssh


### quick start


### 支持说明
  - java version : jdk8
  - spring and springmvc version : 4.0.4.release
  - tomcat version : 8.5.34
  
### 接入DMP 


#### 注册到 eureka

 - add maven dependency
  ```xml
 
      <dependency>
          <groupId>com.netflix.eureka</groupId>
          <artifactId>eureka-client</artifactId>
          <version>1.4.12</version>
      </dependency>
      
      <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.16.22</version>
      </dependency>
      
      <dependency>
          <groupId>com.netflix.archaius</groupId>
          <artifactId>archaius-core</artifactId>
          <version>0.7.6</version>
      </dependency>
      
  ```
 - 在resource下 **config.properties** 
 - 添加 listener **EurekaInitListener**
 - 在 **web.xml** 配置 listener **EurekaInitListener** 
  ```xml
    <listener>
    	<listener-class>io.daocloud.dmp.demo.config.eureka.EurekaInitListener</listener-class>
    </listener>
  ```
 - 启动app
 
#### 接入apollo,获取配置信息
 - add apollo 依赖
  ```xml
    <dependency>
       <groupId>com.ctrip.framework.apollo</groupId>
       <artifactId>apollo-client</artifactId>
       <version>1.1.0</version>
    </dependency>
  ```
 - 添加 apollo 配置类 **ApolloConfig** , **TestJavaConfigBean**
 - 添加 启动参数 **-Denv=dev -Dapp.id=dmp -Dapollo.meta=http://192.168.1.217:8080**
 
 #### 接入是skywalking
 - 下载好skywalking-agent jar 文件
 Linux Tomcat 7, Tomcat 8,修改 tomcat/bin/catalina.sh,在首行加入如下信息:
 ```bash
  CATALINA_OPTS="$CATALINA_OPTS -javaagent:/path/to/skywalking-agent/skywalking-agent.jar"; export CATALINA_OPTS
 ```