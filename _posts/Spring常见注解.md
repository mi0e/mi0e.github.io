---
title: Spring常见注解
date: 2023-08-14 23:17:52
tags:
---

## Spring

|注解|说明|
|:-:|:-:|
|@Conmponent、@Controller、@Service、@Repository|使用在类上用于实例化Bean|
|@Autowired|使用在字段上用于根据类型依赖注入|
|@Qualifier|结合@Autowired一起使用用于根据名称进行依赖注入|
|@Scope|标注Bean的作用范围|
|@Configuration|指定当前类是一个 Spring 配置类，当创建容器时会从该类上加载注解|
|@ComponentScan|用于指定 Spring在初始化容器时要扫描的包|
|@Bean|使用在方法上，标注将该方法的返回值存储到Spring容器中|
|@Import|使用@Import导入的类会被Spring加载到IOC容器中|
|@Aspect、@Before、@After、@Around、@Pointcut|AOP|

## SpringMVC

|注解|说明|
|:-:|:-:|
|@RequestMapping|用于映射请求路径，可以定义在类上和方法上。用于类上，则表示类中的所有的方法都是以该地址作为父路径|
|@RequestBody|注解实现接收http请求的json数据，将json转换为java对象|
|@RequestParam|指定请求参数的名称|
|@PathViriable|从请求路径下中获取请求参数(/user/(id])，传递给方法的形式参数|
|@ResponseBody|注解实现将controller方法返回对象转化为json对象响应给客户端|
|@RequestHeader|获取指定的请求头数据|
|@RestController|@Controller + @ResponseBody|

## SpringBoot

|注解|说明|
|:-:|:-:|
|@SpringBootApplication|启动SpringBoot，包含以下三个注解|
|@SpringBootConfiguration|结合了 @Configuration ，实现配置文件功能|
|@EnableAutoConfiguration|打开自动配置功能，也可以关闭某个自动配置的类|
|@ComponentScan|组件扫描|
