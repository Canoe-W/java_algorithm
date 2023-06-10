# Maven

安装：黑马程序员

要设置环境变量和仓库位置

然后IDEA可以使用Maven快速创建项目，maven主要用来管理jar包，在pom文件中设置dependencies

优先顺序：

![Snipaste_2023-06-05_19-55-03](E:\java_algorithm\学习截图\Snipaste_2023-06-05_19-55-03.png)

声明优先看的是id不同的，特殊优先看的是id相同版本不同的



隐藏依赖：不透明

```
<optional>true<optional>
```







排除依赖：不需要

```
<exclusions>
	<exclusion>
		配置，但是没有版本
	<exclusion>
<exclusions>
```

依赖范围

```
<scope> <scope>
compile test provided runtime
test和provided不传递
```



生命周期和插件

生命周期：项目运行的每一步，比如测试、安装之类的，很细有表可以参照

插件：在对应生命周期干指定的行为，有产出，比如打包jar包之类的产物





## 高级

模块拆分。放到ssm后面看



# Postman







# SSM





# Spring boot



parent :用来统一稳定兼容的jar包版本，用于减少依赖产生的冲突

start：用来定位依赖，用于减少依赖

SpringBoot的引导类是Boot工程的执行入口，运行main方法就可以启动项目

SpringBoot工程运行后初始化Spring容器，扫描引导类所在包加载bean

如果不在同一级包或者子包下是无法扫描到的，解决方法----->



内嵌tomcat,将tomcat服务器作为对象运行，并将该对象交给Spring容器管理

变更内嵌服务器思想是去除现有服务器，添加全新的服务器，exclusions



## Rest

```
设置http请求动作（动词） 设定请求参数（路径变量）
@RequestMapping
方法注解 SpringMVC控制器方法定义上方 设置当前控制器方法请求访问路径
value(默认):请求访问路径
method:http请求动作，标准动作(GET,POST,PUT,DELETE)
@PathVariable
形参注解 SpringMVC控制器方法形参定义前面
绑定路径参数与处理器方法形参之间的关系，要求路径参数名与形参名一一对应
```



```java
@RequestMapping(value="/users/{id}",method=RequestMethod.DELETE)
@ResponseBody
public String delete(@PathVariable Integer id){
    System.out.println("user delete..."+id);
    return "{'module':'user delete'}";
}
```



```
@RequestBody,@RequestParam,@PathVariable
区别
@RequestParam用于接收url地址传参或表单传参
@RequestBody用于接收json数据
@PathVariable用于接收路径参数，使用{参数名称}描述路径参数
应用
后期开发中，发送请求参数超过1个时，以json格式为主，@RequestBody应用较广
如果发送非json格式数据，选用@RequestParam接受请求参数
采用RESTful进行开发，当参数数量较少时，例如一个，可以采用@PathVariable接收请求路径变量，通常用于传递id值
```

![Snipaste_2023-06-06_10-18-24](E:\java_algorithm\学习截图\Snipaste_2023-06-06_10-18-24.png)

简化提取融合

## 基础部分



### 基础配置

![Snipaste_2023-06-06_10-36-32](E:\java_algorithm\学习截图\Snipaste_2023-06-06_10-36-32.png)



修改配置

修改服务器端口

```
server.port=80//适用于tomcat
```



Spring Boot 默认端口为8080，如果需要更改默认启动端口，可以通过多种方式来实现：

1. 在 application.properties 文件中添加配置

在 Spring Boot 项目的 src/main/resources 目录下，新建 application.properties 文件，并在其中添加以下配置：

```
server.port=8081
```

其中，server.port 代表 Spring Boot 应用的端口号，可以根据实际情况选择任意未被占用的端口号。

2. 在 application.yml 文件中添加配置

在 Spring Boot 项目的 src/main/resources 目录下，新建 application.yml 文件，并在其中添加以下配置：

```yaml
server:
  port: 8081
```

3. 通过命令行参数设置

通过命令行参数来指定 Spring Boot 应用的端口号，如下所示：

```
java -jar myproject.jar --server.port=8081
```

其中，myproject.jar 代表可执行的 Spring Boot 项目的名称。

4. 通过环境变量设置

可以通过设置环境变量来指定 Spring Boot 应用的端口号，如下所示：

```
SERVER_PORT=8081 java -jar myproject.jar
```

其中，SERVER_PORT 代表 Spring Boot 应用的端口号，myproject.jar 代表可执行的 Spring Boot 项目的名称。

以上四种方法中，推荐使用 application.properties 或 application.yml 文件中的方式来设置 Spring Boot 应用的端口号，因为这种方式既简单又方便，在实践中被广泛采用。



指定SpringBoot配置文件

```
Setting->Project Structure->Facets
对应工程/项目
Customize Spring Boot
选择配置文件
```



yaml书写规范

```
yam1语法规则
●大小写敏感
●属性层级关系使用多行描述,每行结尾使用冒号结束
●使用缩进表示层级关系，同层级左侧对齐,只允许使用空格(不允许使用Tab键)
●属性值前面添加空格 (属性名与属性值之间使用冒号+空格作为分隔)
●#表示注释
```

![Snipaste_2023-06-06_22-40-46](E:\java_algorithm\学习截图\Snipaste_2023-06-06_22-40-46.png)

![Snipaste_2023-06-06_22-41-38](E:\java_algorithm\学习截图\Snipaste_2023-06-06_22-41-38.png)



```
@Value("${一级属性名.二级属性名...[i]}")数组可选
```

1.在配置文件中可以使用${属性名}方式引用属性值
2.如果属性中出现特殊字符，可以使用双引号包裹起来作为字符解析



![Snipaste_2023-06-06_22-55-40](E:\java_algorithm\学习截图\Snipaste_2023-06-06_22-55-40.png)



为了更方便，下面将选择部分封装，少记类名

![Snipaste_2023-06-06_23-04-55](E:\java_algorithm\学习截图\Snipaste_2023-06-06_23-04-55.png)

1.使用@ConfigurationProperties注解绑定配置信息到封装类中
2.封装类需要定义为Spring管理的bean,否则无法进行属性注入



### SpringBoot整合Junit

1.导入测试对应的starter
2.测试类使用@SpringBootTest修饰
3.使用自动装配的形式添加要测试的对象



1.测试类如果存在于引导类所在包或子包中无需指定引导类
2.测试类如果不存在于引导类所在的包或子包中需要通过classes属性指定引导类





### SpringBoot整合MyBatis

导入模块选择MyBatis Framework和mysql driver

在配置文件设置数据源参数

定义数据层接口与映射配置

```java
@Mapper
public interface UserDao{
    @Select("select * from user")
    public List<User> getAll();
}
```

测试类中注入dao接口，测试功能

```java
@SpringBootTest
class xxxApplicationTests{
    @Autowired
    private BookDao bookDao;
    @Test
    public void testGetById(){
        Book book =bookDao.getById(1);
        System.out.println(book);
    }
}
```

mysqyl8以上要设置时区



MyBatisPlus在Idea目前用不了

总的来说就是导入坐标，然后extends那个什么Mapper(类名啥的)，@table指定表名，配置文件里面也可以写前缀，后面就正常用

### SpringBoot整合Druid



导包，设配置







### 基于SpringBoot的SSMP整合案例

1. pom . xml
配置起步依赖
2. application . yml
设置数据源、端口、框架技术相关配置等
继承BaseMapper.设置@Mapper
4. dao测试类
5. service
调用数据层接口或MyBatis -Plus提供的接口快速开发
6. service测试类
7， controller
基于Restful开发，使用Postman测试跑通功能
8.页面
放置在resources目录下的static目录中





## 运维实用篇

### 打包与运行

#### windows版本

##### 打包

lifecycle里面有package打包

要会跳过测试



```
1.对SpringBoot项目打包 执行maven构建指令package
mvn package
2.运行项目 执行启动命令
java -jar springboot.jar
```



确保有maven插件被打包，确保有主清单，会将用的jar包也打包进去，在boot-inf



jarlauncher



windows端口被占用解决办法

```
#查询端口
netstat - ano
#查询指定端口
netstat -ano |findstr "端口号"
#根据进程PID查询进程名称
tasklist |findstr "进程PID号"
#根据PID杀死任务
taskkill /F /PID "进程PID号"
#根据进程名称杀死任务
taskkill -f -t -im "进程名称'

```



### 属性配置

```
java -jar xxx.jar --server.port=8080 单个属性
多个属性 属性间使用空格分隔 命令行属性优先级更高，会覆盖配置文件里面的属性 有一个文档里里面有属性优先级，可以查询，其实不是覆盖，是先查询到
```



临时属性在开发环境中 在configuration里面配置环境参数

编程启动函数里面可以删去args，拒绝了传参



配置文件4级分类

为了不同类型的人员使用不同的配置

在config文件夹里面写一个application.yml      config级别更高     开发中好像不用这个？不清楚

和打包后的jar包同级目录下有一个yml配置文件可以覆盖、先查询到，级别更高

主要是叠加覆盖

```
配置文件分类
1. SpringBoot中4级配置文件
1级: file : config/application.yml [最高]
2级: file : application. yml
3级: classpath: config/application.yml
4级: classpath: application. yml [最低]
2.作用:
◆1级与2级留做系统打包后设置通用属性 , 1级常用于运维经理进行线上整体项目部署方案调控
◆3级与4级用于 系统开发阶段设置通用属性，3级常用于项目经理进行整体项目属性调控
不同目录设置不同的密码，保证运维安全
同一级别properties文件级别更高
```





自定义配置文件

```
在configuration里面通过启动参数
--spring.config.name=xxx(自定义的名字不用加后缀) 对properties和yml都有效
--spring.config.location=classpath:/ebank.yml,classpath:/ebank-server.yml 根据文件路径去找,多个配置文件，最后一个生效
```

原则，只增加不改原来的

```
单服务器项目:使用自定义配置文件需求较低
多服务器项目:使用自定义配置文件需求较高，将所有配置放置在一个目录中，统一管理
基于SpringCloud技术，所有的服务器将不再设置配置文件，而是通过配置中心进行设定，动态加载配置信息
```



### 多环境开发（yaml版&properties版本）



```
在yml文件中多个环境用---区分环境边界
通常是应用环境（公共配置），设置环境：生产环境pro、开发环境dev、测试环境test
环境区别在于加载的配置属性不同，相同的地方在最上面设置一遍即可

spring:
 profiles:
  active: pro#用哪个写哪个
---
server:
 port: 80

spring:
 config:
  activate:
   on-profile: pro#这个是用于设置环境名称
```

对于隐私数据,我们分为三个文件分开配置，作为独立文件管理，加个后缀，主配置文件设置公共配置



properties版本

具体操作和yml一样



书写技巧

```
●根据功能对配置 文件中的信息进行拆分,并制作成独立的配置文件，命名规则如下
application-devDB.yml
application-devRedis.yml
application-devMVC.yml
●使用include属性在激活指定环境的情况下，同时对多个环境进行加载使其生效，多个环境间使用逗号分隔
spring:
 profiles :
  active: dev
  include: devDB , devRedis , devMVC
后加载覆盖前加载的吗，active覆盖include
group属性
"dev": 
"pro": 
这样的话主配置顺序在前面，顺序更合理了

```



多环境开发控制

maven配置为主，springboot依赖于maven的坐标

maven与springboot多环境兼容的时候，在maven中设置多环境属性

```
<profiles>
	<profile>
		<id>dev_ env</id>
		<properties>
			<profile.active>dev</profile.active>
		</properties>
		<activation>
			<activeByDefault>true</activeByDefault>
		</activation>
	</profile>
	<profile>
		<id>pro_ env</id>
		<properties>
			<profile.active>pro/profile.active>
		</properties>
	< /profile>
	<profile>
		<id>test_ env</id>
		<properties>
			<profile. active>test</profile .active>
		</ properties>
	</profile>
</profiles>

```

在springboot中引用maven属性

```
spring:
 profiles:
  active: @profile.active@
```

修改pom文件后要compile重新编译才能重新加载更新配置（IDEA环境中）



### 日志基础操作



#### 日志基础操作



在controller类里面增加日志对象

```java
//创建记录日志的对象
private static final Logger log=LoggerFactory.getLogger(BookController.class);
//具体接口
log.debug("sss");
log.info("sss");
log.warn("sss");
log.error("sss");
//默认看info级别以上的，想看debug要在yml文件中配置debug: true

```



推荐设置

```
#开启debug模式，输出调试信息，常用于检查系统运行状况
debug: true

#设置日志级别，root表示根节点，即整体应用日志级别
logging:

 group:#设置包名
  ebank: 
  iserver: 
  
 level:
  root: debug
  #设置某个包的日志级别
  com.xx.xx: debug
  #设置分组，对某个组设置日志级别
  ebank: warn
  

```



debug级别不是很推荐设置，太多

一般用info



#### 快速创建日志

为了少写那一行代码

```
导入lombok插件依赖
BookController类前面加@Slf4j，对象名还是叫log直接用就可以了
```



#### 日志输出格式控制(看个乐子就行)

```
时间 级别 PID 所属线程 所属类/接口名（简化包名书写为字母） 日志信息
```

可改可不改

```
pattern:
 console: "%d %clr(%p) ---[%16t] %clr(%-40.40c){cyan} : %m %n"
```

放在logging里面



#### 文件记录日志(很实用)

```
设置日志文件
logging:
 file:
  name: server.1og
日志文件详细配置
logging: 
 file:
  name: server.1og
 logback:
  rollingpolicy:
   max-file-size: 3KB
   file-name-pattern: server.%d{yyy-MM-dd}.%i.1og 

```

在项目根目录下可以查看



## 开发使用篇

### 热部署

#### 自动启动

需要在pom文件里面添加插件

在setting-build,execution,deployment-compile里面选择build project automatically

然后在advanced setting中勾选allow auto-make to...

#### 热部署范围

有默认不触发重启的目录列表

我们可以自定义不参与重启排除项

```
devtools:
 restart:
  exclude: public/**,static/**
```



#### 取消热部署

enabled: false

或者在springboot启动文件里面设置properties，层级更高



### 第三方Bean绑定

```
@Component是标注类，注册为Bean,@Bean是标注方法返回的对象，将对象注册为Bean
```



```
@ConfigurationProperties注解绑定自定义的第三方Bean

注解三连
@Component
@Data
@ConfigurationProperties

在启动文件中有@EnableConfigurationProperties这个可以将使用@ConfigurationProperties注解对应的类加入Spring容器中，不能与@Component同时使用
```



#### 宽松绑定

```
@ConfigurationProperties绑定属性名支持属性名宽松绑定
即忽略大小写和下划线中划线等等
注意事项：宽松绑定不支持注解@Value引用单个属性的方式
eg.@Value("${servers.ipaddress}")
prefix绑定
绑定前缀名命名规范：仅能使用纯小写字母、数字、中划线作为合法的字符
```



### 常用计量单位

```
SpringBoot支持 JDK8提供的时间与空间计量单位
@Component
@Data
@ConfigurationProperties (prefix = "servers")
public class ServerConfig {
	private String ipAddress;
	private int port;
	private 1ong timeout;
	@DurationUnit(ChronoUnit .MINUTES)
	private Duration serverTimeOut ; 
	@DataSizeUnit (DataUnit .MEGABYTES)
	private DataSize dataSize ;
}

```



### Bean属性校验

```
1.启用Bean属性校验
●导入JSR303 与Hibernate校验框架坐标
●使用@Validated注解启用校验功能
●使用具体校验规则规范数 据校验格式
```



```
①:添加JSR303规范坐标与Hibernate校验框架对应坐标
<dependency>
	<groupId>javax.validation</ groupId>
	<artifactId>validation-api</artifactId>
</dependency>
<dependency>
	<groupId>org.hibernate.validator</ groupId>
	<artifactId>hibernate-validator</artifactId>
</dependency>

```



```
③:设置校验规则
@Component
@Data
@ConfigurationProperties(prefix = "servers")
@Validated
public class ServerConfig {
	@Max(value = 400,message ="最大值不能超过400" )
	private int port;
}
```



进制数据转化规则

设密码要加双引号，不然以数值处理的地方0开头会被抹掉变成8进制

```
0(0-7)八进制
0x(0-9,a-f)十六进制
●字面值表达方 式
boolean: TRUE
#TRUE, true, True, FALSE, false, False均可
float: 3.14
#6.8523015e+5
#支持科学计数法
int: 123
#0b1010_ 0111_ 0100_ 1010_ 1110
#支持二进制、八进制、十六进制
nu1l: ~ 
#使用~表示ull
string: HelloWorld
#字符串可以直接书写
string2: "Hello World"
#可以使用双引号包裹特殊字符
date: 2018-02-17
#日期必须使用yyyy-MM- dd格式
datetime: 2018-02 -17T15:02:31+08:00 #时间和日期之间使用T连接， 最后使用+代表时区
1.注意yaml文件中对于数字的定义支持进制书写格式，如需使用字符串请使用引号明确标注
```



### 测试



```
1. web环境模拟测试
●设置测试端口
●模拟测试启动
●模拟测试匹配 (各组成部分信息均可匹配)
```



#### 加载测试专有属性

在启动测试环境时可以通过properties参数设置测试环境专用的属性

```
@SpringBootTest(properties = {"test . prop=testValue1"})
public class PropertiesAndArgsTest {
	@Value("${test. prop}")
	private String msg;
	@Test
	void testProperties(){
		System. out . print1n(msg);
	}
}
```

 优势: 比多环境开发中的测试环境影响范围更小，仅对当前测试类有效



在启动测试环境时 可以通过args参数设置测试环境专用的传入参数

```
@SpringBootTest(args = {"--test. arg=testValue2"})
public class PropertiesAndArgsTest {
	@Value("${test.arg}")
	private String msg;
	@Test
	void testArgs(){
		System. out . print1n(msg);
}
```



同名优先级：args>properties>yml



#### 加载测试专用配置

Bean

使用@Import注解加载当前测试类专用的配置

```
@SpringBootTest
@Import({MsgConfig.class})
public class ConfigurationTest {
	@Autowired
	private String msg;
	@Test
	void testConfiguration(){
		System.out.println(msg);
	}
}
```



```
@Configuration
public class MsgConfig {
	@Bean
	publle string msg(){
		return "bean msg";
	}
}
```



#### 测试类中启动Web环境

web环境模拟测试
模拟端口

```
@SpringBootTest (webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
	public class WebTest {
	@Test
	void testRandomPort () {
}
```

有MOCK,DEFINED_PORT,RANDOM_PORT,NONE

#### 发送虚拟请求



```
@RestController
@RequestMapping("/books")
public class BookController {
    @GetMapping
	public string getById(){
		system.out.printIn("getById is running ...."):
		return "springboot";
	}		
}
```

●虚拟请求测试

```
@SpringBootTest (webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
//开启虚规MVC调用
@AutoConfigureMockMvc
public class WebTest {
	@Test
	//注入虚规MVC调用对象
	public void testWeb(@Autowired MockMvc mvc) throws Exception {
		//创建虚拟请求，当前访问/books
		MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
		//执行请求
		ResultActions action = mvc.perform(builder); 
	}
}
```



#### 匹配响应执行状态

虚拟请求状态匹配

```
@Test
public void testSataus (@Autowired MockMvc mvc) throws Exception {
	MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books"); 
	ResultActions action = mvc.perform(builder );
	//匹配执行状态(是否预期值)
	//定义执行状态匹配器
	StatusResultMatchers status = MockMvcResultMatchers.status();
	//定义预期执行状态
	ResultMatcher ok = status.isOk();
	//使用本次真实执行结果与预期结果进行比对
	action.andExpect(ok);
}
```



#### 匹配响应体(json)

虚拟请求体(json) 匹配

这里那个网页有返回Book类型

```
@Test
public void testJson(@Autowired MockMvc mvc) throws Exception {
	MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books"); 
	ResultActions action = mvc.perform(builder);
	//匹配执行结果(是否预期值)
	//定义执行结果匹配器
	ContentResultMatchers content = MockMvcResultMatchers.content();
	//定义预期执行结果
	ResultMatcher result = content .json("{\"id\" :1, \"name\" :\"SpringBoot2\"}");
	//使用本次真实执行结果与预期结果进行比对
	action. andExpect(result);
}

```



#### 匹配响应头

```
@Test
void testContentType (@Autowired MockMvc mvc) throws Exception {
	MockHttpServletRequestBuilder bui1Her = MockMvcRequestBuilders. get( urlTemplate: "/books"); 
	ResultActions action = mvc. perform(bui1der);
	//设定预期值与真实值进行比较， 成功测试通过，失败测试失败
	//定义本次调用的预期值
	HeaderResultMatchers header = MockMvcResultMatchers.header();
	ResultMatcher contentType = header . string( name: "Content-Type", value: "application/json");
	//添加预计值到本次调用过程中进行匹配
	action.andExpect(contentType);
}
```



#### 业务层测试事务回滚



```
数据层测试事务回滚
●为测试用例添加事务, SpringBoot会对测试用例对应的事务提交操作进行回滚
@SpringBootTest
@Transactional
public class DaoTest {
	@Autowired
	private BookService bookService;
}
●如果想在测试用例中提交事务，可以通过@Rollback注解设置
@SpringBootTest
@Transactional
@Rollback(false)
public class DaoTest {
}

```

还是会占用id行数，但是数据不计入

#### 测试用例设置随机数据

在yml设置配置

```
testcase:
 book:
  id: ${random.int}
  可以指定范围int(10) int(5,10)也可以中括号，只要是分隔符就行，比如@，!,可以自定义
  前面也可以加固定前缀
  name: ${random.value}
  uuid: ${random.uuid}
  publishTime: ${random.long}
```



找一个实体类封装成数据

```
@Component
@Data
@ConfigurationProperties(prefix="testcase.book")
```



### 数据层解决方案 SQL NoSQL

#### 

```
Druid+MyBatis+MySQL
```

数据源，持久化技术，数据库

druid-starter一定要导入

如果没有druid的话我们使用的是内置的Hikari

#### 内置数据源

SpringBoot有三种内嵌的数据源对象

```
HikariCP(默认)
Tomcat提供的DataSource
Commons DBCP
```

Hikari里面不能放url，要放外层，原理篇讲



#### JdbcTemplate



```
@SpringBootTest
class Springboot15SqlApplicationTests {
	@Autowired
	private JdbcTemplate jdbcTemplate;
	@Test
	void testJdbc(){
		String sql = "select * from tbl_ book where id = 1";
		List<Book> query = jdbcTemplate . query(sql, new RowMapper<Book>() {
			@Override
			public Book mapRow( ResultSet rs, int rowNum) throws SQLException {
				Book temp = new Book();
				temp . setId(rs . getInt("id"));
				temp. setName (rs . getString( " name"));
				temp.setType(rs . getString( "type" ));
				temp. setDescription(rs . getString( "description"));
				return temp;
			}
		});
		System.out.println(query); 
	}
}

```



```

<dependency>
	<groupId>org . springfr amework . boot</ groupId>
	<artifactId>spring- boot -starter- jdbc</ artifactId>
</dependency>

```

对此还可以个性化设置，比如查询超时时间，最大行数和缓存行数



#### H2数据源(不是很重要，看看就行)

三种内置：H2,HSQL,Derby

内存小，在内存中运行，脱离文件，便于测试

主要讲H2

jar包和管理

线上运行务必关闭，有安全隐患





### Redis   NoSQL

Redis是一款key-value存储结构的内存级NoSQL数据库

支持多种数据存储格式，持久化，集群

#### 下载安装与基本使用





#### SpringBoot整合Redis

NoSQL redis

导入包，看配置，设置yml

直接输入redis去配yml

装配，设置对象，然后使用

```
@Autowired
private RedisTemplate redisTemplate;

@Test
void set(){
	ValueOperation ops = redisTemplate.opsForValue();
	ops.set("age",41);
}
```

中文会出现cmd转码，使用--raw显示中文，可能会乱码，可以使用chcp 65001临时改变cmd的编码

最好使用StringRedisTemplate,不然客户端可能会出现乱码

ops*: 各种操作

#### 读取Redis的客户端



RedisTemplate以对象为操作对象，Redis内部有自己的序列化方式，StringRedisTemplate以字符串为操作对象，与Redis客户端操作等效

所以一般使用StringRedisTemplate



#### 操作Redis客户端实现技术切换（jedis）

默认使用lettcue

client-type: jedis

spring兼容问题

**lettcus与jedis区别**

jedis连 接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响。

lettcus基于Netty框架进行与Redis服务器连接，底层设计中采用StatefulRedisConnection。StatefulRedisConnection自身是线程安全的，可以保障并发访问安全问题，所以-一个连接可以被多线程复用。当然lettcue也支持多连接实例一起工作。



### Mongodb

开源，高性能，无模式的文档型数据库，NoSQL数据库产品中的一种，是最像关系型数据库的非关系型数据库

无模式：无模式数据库 (Schemaless database) 是 NoSQL 数据库的一种，它相较于传统的关系型数据库，不需要预定义固定的数据模型和表结构。这使得无模式数据库可以快速地适应不同类型的数据结构，同时提高了扩展性和灵活性。

无模式数据库通常使用文档型或键值对的方式来存储数据，它们特别适用于存储半结构化和非结构化的数据。与关系型数据库通常需要进行多表关联以获取所需数据不同，无模式数据库的数据可以在同一文档内或同一键值对下进行存储，降低了查询的复杂度，提高了查询效率。

此外，无模式数据库还支持分布式数据存储和高可用性，可以实现数据的动态扩展和负载均衡，在处理海量数据时具有明显的优势。常见的无模式数据库有 MongoDB、CouchDB、Riak 等。

文档型：文档型数据库 (Document-oriented database) 是 NoSQL 数据库的一种，它以半结构化的文档格式来存储数据。正如其名称所示，它是以文档为数据存储的单元。每个文档可以具有不同的结构和格式，不同于关系型数据库使用表来存储结构化数据。

文档型数据库采用的是键值对的方式来存储数据。一个文档可以有多个键值对，每个键值对可以包含一个值，一个值可以是一个字符串、数字、布尔类型等，甚至可以是一个嵌套的文档或数组。

文档型数据库具有很好的横向扩展和动态扩展能力，这使得它在面对海量数据的处理中具有很好的性能优势。常见的文档型数据库有 MongoDB、Couchbase、CouchDB 等。



#### mongodb操作

使用robo3t,navicat也可以

创建数据库，文档（collection)



```
db.book.save({"name":"springboot"})//格式按照json
```



```
db.getCollection('book').find({})
db.book.find()
db.book.remove({type:"xxx"})
db.book.update({name:"xxx"},{$set:{name:"ssss"}})修改满足条件的第一条
```



出来的数据格式像json有不是json,叫bson

```
1.基础查询
◆查询全部: db.集合. find();
◆查第一条: db.集合.find0ne()
◆查询指定数量文档: db.集合. find() . limit(10)//查10条文档
◆跳过指定数量文档: db.集合. find(). skip(20)//跳过20条文档
统计: db.集合. count() .
◆排序: db.集合. sort({age:1})//按age升序排序
◆投影: db.集合名称.find(条件, {name:1, age:1})//仅保留name与age域
2.条件查询 !
◆基本格式: db. 集合. find({条件})
◆模糊查询: db.集合. find({域名:/正则表达式/})//等同SQL中的1ike,比like强大，可以执行正则所有规则
◆条件比较运算: db.集合. find({域名:{$gt:值}})//等同SQL中的数值比较操作,例如: name>18
◆包含查询: db. 集合. find({域名:{$in:[值1,值2]}})//等同于SQL中的in
◆条件连接查询: db. 集合.find({$and:[{条件1}, {条件2}]})//等同于SQL中的and、or
```



#### 整合

导入对应的坐标

在yml文件输入mango

设置配置mongodb

```
uri: mongodb://localhost/cira
```

 

自动装配mongoTemplate



### ES

Elasticsearch

分布式全文搜索引擎

索引 倒排索引 创建文档 使用文档

核心观念： 倒排索引

es8适用于jdk17+

es7可以用jdk1.8

#### 索引操作(在springcloud里面有)

ik分词器

postman演示操作，看一下就好，之后再学

es目录下不能有空格

设置索引创建规则

#### 文档操作

数据选json

创建

```
post  http://localhost:9200/books/_doc/id       _doc不加id则是生成随机id
/_create/id
```

查询

get       _search

get       _search?q=name:springboot



删除

delete    _doc/id



修改

```
put       _doc/id    全量修改
post      _update/id     部分修改
```



#### 整合

pom文件导入包

yml文件设置配置

启动包生成对象

```
@Autowired
private ElasticsearchRestTemplate template;
用于操作 但是过时
新版本有高低级别

private RestHighLevelClient client;


springboot已经整合了高版本的es
写一个ESConfig配置类，写一个初始化client的@Bean
```



#### 添加文档

```
@Test
void testCreateIndexByIK() throws IOException{
	HttpHost host=HttpHost.create("http://localhost:9200");
	RestClientBuilder builder = RestClient.builder(host);
	RestHighLevelClient client=new RestHighLevelClient(builer);
	//客户端操作
	CreateIndexRequest request=new CreateIndexRequest("books");
	//设置要执行的操作
	String json="";
	//设置请求参数。参数类型json数据
	request.source(json,XContentType.JSON);
	//获取操作索引的客户端对象，调用创建索引操作】
	client.indices().create(request,RequestOptions.DEFAULT);
	//关闭客户端
	client.close();
}

```

```
批量添加文档
//批量添加文档
@Test
void testCreateDocAl1() throws I0Exception {
	List<Book> bookList = bookDao. selectList(nu11);
	BulkRequest bulk = new BulkRequest();
	for (Book book : bookList) {
		IndexRequest request = new IndexRequest( "books"). id(book.getId() . toString());
		String json = JSON. toJSONString(book);
		request . source(json, XContentType .JSON) ;
		bulk . add(request);
	}
	client . bulk(bu1k, RequestOpt ions .DEFAULT);
}

```



#### 查询文档

这两个等学会了再看，总的就是还是利用es在启动类里面写写写进行操作

基本都是使用json格式

```
按id查询文档
@Test
void testGet() throws I0Exception {
	GetRequest request = new GetRequest( "books","1");
	GetResponse response = client. get( request, RequestOptions .DEFAULT);
	String json = response . getSourceAsString();
	System. out . println(json);
}
```



```java
按条件查询文档
@Test
void testSearch() throws IOException {
	SearchRequest request = new SearchRequest( "books");
	SearchSourceBuilder builder = new SearchSourceBuilder();
	builder . query(QueryBuilders . termQuery("a11", "java"));
	request . source(builder);
	SearchResponse response = client . search( request, RequestOptions . DEFAULT);
	SearchHits hits = response . getHits(); 
	for (SearchHit hit : hits) {
		String source = hit. getSourceAsstring();
		Book book = JSON. parseobject(source, Book . class);
		System . out . println(book);
	}
}
```



### 整合第三方技术

#### 缓存







#### 任务









#### 邮件











#### 消息





