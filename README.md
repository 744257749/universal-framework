# universal-framework
# Spring Boot通用快速开发框架

###   框架描述：
   通用快速开发框架是一套轻量级的权限系统，主要包括用户管理、角色管理、部门管理、菜单管理、SQL监控、定时任务、参数管理、字典管理、文件上传、系统日志、文章管理、APP模块等功能。还拥有多数据源、数据权限、Swagger支持、Redis缓存动态开启与关闭、统一异常处理、多模块、云存储、代码生成器等技术特点
   
------------

### 技术选型：
1.    核心框架：Spring Boot 2.0.2
2.    安全框架：Apache Shiro 1.4
3.    视图框架：Spring MVC 5.0.6
4.    持久层框架：MyBatis 3.4.6 + MybatisPlus2.1.9
5.    分布式集群调度：Quartz 2.3
6.    数据库连接池：Druid 1.1.10
7.    分布式缓存：Redis 4.0.9
8.    日志管理：SLF4J 1.7、Log4j
9.    单元测试：JUnit 4.12
10.   API接口文档：Swagger 2.7.0
11.   页面交互：Vue 2.x + Bootstrap+ HTML5 + CSS3

### 项目特点：
1.    通用快速开发框架采用SpringBoot、MyBatis、Shiro等技术开发，极低门槛，拿来即用。设计之初，就非常注重安全性，为企业系统保驾护航，让一切都变得如此简单。
2.    灵活的权限控制，可控制到页面和按钮，满足绝大部分的权限需求。
3.    完善的部门管理及数据权限，通过注解实现数据权限的控制。
4.    完善的XSS防范及脚本过滤，彻底杜绝XSS攻击。
5.    支持MySQL、Oracle、SQL Server等主流数据库。
6.    支持分布式部署，session存储在Redis。
7.    友好的代码结构及注释，便于阅读及二次开发。
8.    页面交互使用Vue2.x，极大提高开发效率。
9.    引入Swagger文档支持，方便编写API接口文档。
10.   引入Quartz定时任务，可动态完成任务的添加、修改、删除、暂停、恢复及日志查看等功能
11.   提供代码生成器，生成entity、xml、dao、service、html、js、sql等代码。只需编写30%左右代码，其余代码交给系统自动生成，可快速完成开发任务。

### 数据权限设计：
1.    管理员管理、角色管理、部门管理，可操作本部门及子部门数据。
2.    菜单管理、定时任务、参数管理、字典管理、系统日志，没有数据权限。
3.    业务功能，按照用户数据权限查询、操作数据（没有本部门数据权限，也能查询本人数据）。

------------

### 项目介绍：
#### 项目一共分为四个模块：
1.    framework-common为公共模块，其他模块以jar包的形式引入进去，主要提供一些工具类，以及framework-admin、framework-api模块公共的entity、mapper、dao、service服务，防止一个功能重复多次编写代码。
2.    framework-admin为后台模块，也是系统的核心，用来开发后台管理系统，可以打包成jar，部署到服务器上运行；或者打包成war，放到Tomcat8.5+容器运行。
3.    framework-api 为接口模块，简化APP开发，为 微信小程序、iOS、Android提供接口，拥有一套单独的用户体系，没有与framework-admin共用用户表。因为framework-admin用户表存放的是企业内部人员账号，具有后台管理员权限，可以登录后台管理系统，而framework-api用户表存放的是真实用户，不具备登录后台管理系统的权限。framework-api主要是实现了用户注册、登录、接口权限认证、获取登录用户等功能，为APP接口的安全调用，提供一套优雅的解决方案，从而简化APP接口开发。
4.    framework-generator为代码生成器模块，只需在MySQL数据库创建好表结构，就可以生成新增、修改、删除、查询、导出等操作的代码，包括entity、mapper、dao、service、controller、页面等所有代码。这是一个项目开发神器。

------------

### 分布式部署：
1.    需要安装Redis，并配置config.properties里的redis信息。
2.    需要配置【framework.redis.open=true】，表示开启Redis缓存。
3.    需要配置【framework.shiro.redis=true】，表示把shiro session存到Redis里。

### 开发调试启动说明：
1.    开发环境任何地方不要包含中文路径。
2.    建好数据表，用代码生成器生成各层次代码。2、将生成的代码依次放到对应的文件夹目录。3、新建菜单，配置用户角色权限（执行代码生成器生成的SQL可以新建菜单）。4、修改controller的每个方法头权限，默认的要根据实际修改。
3.    系统运行在JDK1.8+、MySQL5.5+、Maven3.0+，请按以下步骤配好环境：
4.    修改\universal-framework\framework-admin\src\main\resources的application-dev.yml里的数据库账号和密码
5.    修改\universal-framework\framework-api\src\main\resources的application-dev.yml里的数据库账号和密码
6.    修改\universal-framework\framework-generator\src\main\resources的application.yml里的数据库账号和密码
7.    在universal-framework目录下，执行mvn clean install
8.    导入Maven项目。导入系统前请将全局编码设置为UTF-8，不是GBK。SQL导入也是UTF8编码。

#### 启动项目【framework-admin】：
   Eclipse、IDEA运行AdminApplication.java
   framework-admin访问路径：http://localhost:8080/framework-admin
   swagger文档路径：http://localhost:8080/framework-admin/swagger/index.html
   swagger注解路径：http://localhost:8080/framework-admin/swagger-ui.html
   账号密码：admin/admin

#### 启动项目【framework-api】：
   Eclipse、IDEA运行ApiApplication.java
   framework-api访问路径：http://localhost:8081/framework-api/swagger-ui.html

#### 启动项目【framework-generator】：
   Eclipse、IDEA运行GeneratorApplication.java
   framework-generator访问路径：http://localhost:8082/framework-generator
