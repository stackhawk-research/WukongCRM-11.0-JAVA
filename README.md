# 悟空CRM-11.0


## 悟空CRM介绍


Wukong CRM has a high reputation in China's open source management software industry. At present, the software has reached tens of millions of users, and the download volume of the open source system has reached more than 2 million times, covering a variety of industries such as design manufacturing, service industry, finance, and government agencies. It has reached strategic cooperation with many well-known companies such as Alibaba, Tencent, OPPO, Aerospace Information, and CCTV.

The company has successively won more than 20 honorary awards such as Henan High-tech Enterprise, National 3A Credit Enterprise, IOS9001, and IOS27001 Software Product Certification. It has more than 50 software copyrights. It has been reported by more than 20 domestic media. Since its establishment, the company has taken high technology as its starting point, technology as its core, and perfect after-sales service as its backing. Adhering to the spirit of stability and development, pragmatism and innovation, it has provided services to tens of thousands of companies at home and abroad. In the process of maximizing corporate value, it has achieved the improvement of its own value, achieved the greatest degree of win-win cooperation, and won wide praise and recognition from all walks of life.

Official website address: [http://www.5kcrm.com](http://www.5kcrm.com/)

Demo address: (https://demo10.72crm.com/#/crm)

Account: 18688888888 Password: 123456a

Code Cloud Address: [https://gitee.com/wukongcrm](https://gitee.com/wukongcrm)

QQ Group Communication Group: [1026560336](http:////shang.qq.com/wpa/qunwpa?idkey=13d5e5809eb9feb350336e55c8b7a00b9cb472078b09b4441222a52dd76b278e)

Scan the code to add Xiaowu official customer service WeChat, and invite you to join the WeChat communication group of thousands of people:

<img src="https://images.gitee.com/uploads/images/2019/1231/115927_f9c580c8_345098.png" width="200">

Follow Wukong CRM official account to learn more about Wukong

<img src="https://images.gitee.com/uploads/images/2019/1202/135713_d3566c6a_345098.jpeg" width="200">

:boom: :boom: :boom: Note: Wukong CRM adopts a new front-end and back-end separation mode. The front-end vue packaged file has been integrated in this warehouse code, **you can avoid packaging operations and do not need to run the front-end** . If you need to adjust the front-end code, please download the front-end code separately


(<a href="https://github.com/72wukong/72crm-11.0-web-JAVA" target="_blank">点击下载前端代码</a>) 


## 悟空CRM目录结构

``` lua
wk_crm
├── admin         -- 系统管理模块和用户管理模块
├── authorization -- 鉴权模块，目前仅用于登录鉴权，后期可能有更改
├── bi            -- 商业智能模块
├── core          -- 通用的代码和工具类
├── crm           -- 客户管理模块
├── examine       -- 审批模块
├── gateway       -- 网关模块
├── job           -- 定时任务模块
├── oa            -- OA模块
└── work          -- 项目管理模块


```


## 悟空CRM使用的主要技术栈

| 名称                  | 版本                        | 说明 |
|---------------------|---------------------------|----|
| spring-cloud-alibaba| 2.2.1.RELEASE(Hoxton.SR3) |  核心框架  |
| swagger             | 2.9.2                     |  接口文档  |
| mybatis-plus        | 3.3.0                     |  ORM框架  |
| sentinel            | 2.2.1.RELEASE             |  断路器以及限流  |
| nacos               | 1.2.1.RELEASE             |  注册中心以及分布式配置管理  |
| seata               | 1.2.0                     |  分布式事务 |
| elasticsearch       | 2.2.5.RELEASE(6.8.6)      |  搜索引擎中间件  |
| jetcache            | 2.6.0                     |  分布式缓存框架  |
| xxl-job             | 2.1.2                     |  分布式定时任务框架  |
| gateway             | 2.2.2.RELEASE             |  微服务网关        |
| feign               | 2.2.2.RELEASE             |  服务调用        |


## 悟空CRM项目架构图


<img src="https://images.gitee.com/uploads/images/2020/0910/094237_e7cb3bca_1096736.jpeg" width="650">

## 使用说明

### 一、前置环境
- Jdk1.8
- Maven3.5.0+   
- Mysql5.7.20 （<a href="https://github.com/72wukong/72crm-11.0-Spring/wiki/mysql配置说明" target="_blank">数据库安装注意事项</a>）
- Redis(版本不限)
- Elasticsearch 6.8.6 （<a href="https://github.com/72wukong/72crm-11.0-Spring/wiki/elasticsearch配置说明" target="_blank">环境配置注意事项</a>）
- Seata（1.2.0）（<a href="https://github.com/72wukong/72crm-11.0-Spring/wiki/seata" target="_blank">配置说明</a>）
- Sentinel（1.7.2）（项目中sentinel使用8079端口）
- Nacos（1.2.1)

### 安装

### 一键安装说明

本项目支持Docker一键安装（建议配置 4核16G以以上），[查看具体安装方法](https://github.com/72wukong/72crm-11.0-Spring/wiki/Docker一键安装教程)

### 常见问题

<a href="https://github.com/72wukong/72crm-11.0-Spring/wiki/常见问题以及解决方案" target="_blank">常见问题以及解决方案</a>



### 手动安装说明
     
#### 1. 导入初始化sql,目前项目下gateway模块使用的独立数据库，其他模块使用同一数据库
      

- 安装nacos，新建数据库 `nacos` 在`nacos`数据库中运行` DB/nacos.sql`<br/>
  修改nacos安装目录/conf/application.properties文件，修改数据持久化类型为mysql，添加mysql数据源的url、用户名和密码,配置如下。<br/>
   
```
   spring.datasource.platform=mysql
   db.num=1
   db.url.0=jdbc:mysql://127.0.0.1:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
   db.user=root
   db.password=password
```

- 修改gateway模块数据库配置为`nacos`数据库
- 初始化其余模块数据库：新建数据库 `wk_crm_single` 在`wk_crm_single`数据库中运行 `DB/wk_crm_single.sql`
- 初始化定时任务模块数据库：新建数据库 `xxl_job` 在`xxl_job`数据库中运行 `DB/xxl_job.sql`
- 初始化seata数据库：新建数据库 `seata` 在`seata`数据库中运行 `DB/seata.sql`


#### 2.在项目根目录执行`mvn install`



#### 3.在各个模块下resource目录配置数据库帐号信息以及redis帐号信息`（默认使用的是application-dev.yml配置文件,打包后启动脚本默认使用的application-test.yml配置文件）`



#### 4.在`crm\src\main\resources\application-dev.yml`里面修改elasticsearch配置

        
```
spring.elasticsearch.rest.uris = elasticsearch地址 例：127.0.0.1:9200
spring.elasticsearch.rest.username = elasticsearch用户名 例：elastic 无密码可留空
spring.elasticsearch.rest.password = elasticsearch密码 例: password 无密码可留空

```

注意：elasticsearch [配置注意点](https://gitee.com/wukongcrm/crm_pro/wikis/elasticsearch配置说明?sort_id=2927431)

#### 5.（可选）修改系统中文件上传地址，默认为本地配置，本地上传还需配置公网地址，指向服务器网关

```
crm.upload.config:1                文件上传配置 1:本地 2:阿里云OSS 
crm.upload.oss                     oss上传文件所需配置内容 
crm.upload.oss.bucketName        需要配置两个bucket，0为登录才可访问文件上传地址，1为完全公开文件上传地址
crm.upload.local                   本地上传文件所需配置内容 
crm.upload.local.uploadPath      需要配置两个地址0为登录才可访问文件上传地址，1为完全公开文件上传地址
```

#### 6.（可选）修改jetcache缓存配置详见 <a href="https://github.com/alibaba/jetcache/wiki" target="_blank">官方文档</a> 


#### 7.（可选）项目日志文件在`core\src\main\resources\logback-spring.xml`修改
            

#### 8. 项目打包部署


```
·在项目根目录下执行 mvn clean -Dmaven.test.skip=true package
·然后把对应模块下target文件夹下
·${name}-${version}-SNAPSHOT.zip/tar.gz上传到服务器,例：admin-0.0.1-SNAPSHOT.zip 并将压缩文件解压，检查对应配置文件。

```


#### 9. 项目启动 <br/>


```
先启动nacos,seata,sentinel, elasticsearch,mysql,redis等基础服务
在第八步解压的文件模块下通过执行`sh 72crm.sh start`（windows下直接运行72crm.bat）启动各个模块服务。
其中项目基础模块：gateway，authorization，admin必须启动，其他模块可按需启动。
启动完成后，在浏览器中访问：http://localhost:8443/即可登录系统

```
#### 10. 初始化用户信息<br/>


```
访问http://localhost:8443/  
按照提示初始化超级管理员账号和密码信息，成功之后使用初始化后的管理员账户登录系统添加其他员工，分配权限等

```

#### 11. 升级说明以及注意事项<br/>

```
1、后端代码更新直接下载全量代码替换即可
2、数据库更新请下载 DB/update/V11.x.x.sql，增量执行即可（比如当前版本为V11.0.1，升级为V11.1.0需执行 V11.0.2.sql,V11.1.0.sql）
3、docker更新请使用在线更新或手动将数据库数据备份后执行增量升级SQL，再备份至本地，然后下载新版docker镜像，将增量升级后SQL恢复至新版数据库

```


### 三、其他说明

#### 1.代码生成器及接口文档<br/>


```
代码生成器地址：core\src\test\com\kakarote\generator\Generator.java
接口文档地址`http://localhost:8443/doc.html`
```


#### 2.模块依赖关系 <br/>

```
- 除网关外，其余项目均依赖于admin模块，用于获取当前登录人的信息
- oa模块的任务依赖于work模块，其余一些关联业务功能依赖于crm模块，examine模块
- 商业智能依赖crm,oa模块

```
#### 3.更新日志<br/>
<a href="https://www.72crm.com/upgrade_log" target="_blank">点击查看更新日志</a> 
<br/>
### 四、悟空CRM功能模块预览


![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172541_efed65bd_345098.png "01.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172557_c001d047_345098.png "02.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172612_97363074_345098.png "03.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172625_47a2798b_345098.png "04.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172636_ae5cad59_345098.png "05.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172648_c7928c60_345098.png "06.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172704_ac4c3308_345098.png "07.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172714_84b7ee29_345098.png "08.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172726_4552bddb_345098.png "10.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172736_da77deec_345098.png "11.png")
![输入图片说明](https://images.gitee.com/uploads/images/2020/0928/172745_e22b7a4a_345098.png "12.png")
