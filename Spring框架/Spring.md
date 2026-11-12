
# Bean 线程安全

结论 ：不是线程安全的

成员变量需要考虑线程安全 局部变量就不需要（因为事每个线程的私有的）

无状态：不能修改的 类 是绝对线程安全  果如在bean定义里面加入可修改的成员变量 需要考了是否线程安全


#  什么是AOP 怎么使用呢

 定义 ：面向切面编程 (拦截器的思想) 抽取重复 降低耦合

场景：
1. 记录操作日志 
	使用 AOP中的环绕通知 + 切点式表达  记录参数保存数据库
2. Spring的事务


# 事务失效的场景有哪些

1. 异常捕获处理 自己处理了 然后事务不管；1
2. 抛出检查异常   配置rollbackFor属性为Exception
3. 非public方法 (添加事务通知 前提条件是public)


	# Bean的生命周期
	
1. 通过BeanDefiniton获取bean的定义信息
	
2. **实例化**：调用构造方法创建 Bean 对象（空的）
    
3. **属性注入**：注入 `@Autowired`、`@Value` 等依赖
	
4. 处理Aware接口  
    
5. **初始化前**：执行初始化前的扩展处理
    
6. **初始化**：执行 `@PostConstruct`、`afterPropertiesSet()`、自定义初始化方法
    
7. **初始化后**：执行初始化后的扩展处理，AOP 代理通常在这里生成
    
8. **使用**：Bean 可以被业务代码使用
    
9. **销毁**：容器关闭时执行 `@PreDestroy`、`destroy()`、自定义销毁方法

	1. BeanDefinition（构造函数）
	2. 依赖注入
	3. Aware接口
	4. **BeanPostProcessor** 前置
	5. 初始化方法
	6.  **BeanPostProcessor** 后置
	7. 使用
	8. 销毁

# Spring 中的 循环引用

**@Lazy**延迟缓存
一级缓存：缓存实例
二级缓存：缓存半成品（生命周期没走完）
三级缓存：缓存 bean工厂（解决增强的代理对象 ）


# SpringMVC的执行流程 


1. 浏览器/前端发请求
        ↓
2. DispatcherServlet 接收请求
        ↓
3. HandlerMapping 根据 URL 找到对应的 Handler（Controller 方法）
        ↓
4. HandlerAdapter 负责调用这个 Handler
        ↓
5. HandlerAdapter 解析参数（@RequestParam、@PathVariable、@RequestBody 等）
        ↓
6. 执行 Controller 方法，得到返回值
        ↓
7. 返回值处理：
   - 传统 MVC：ModelAndView → ViewResolver → 渲染 JSP/模板
   - 前后端分离：@ResponseBody / @RestController → HttpMessageConverter
        ↓
8. HttpMessageConverter 把对象转成 JSON（如 Jackson）
        ↓
9. 写入 HttpServletResponse 响应体
        ↓
10. 前端收到 JSON，自己渲染页面


# Springboot自动配置原理


@SpringBootApplication
    ↓
包含 @EnableAutoConfiguration
    ↓
@Import(AutoConfigurationImportSelector.class)
    ↓
读取自动配置清单
（Spring Boot 2.7 前：META-INF/spring.factories
  Spring Boot 3.x：META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports）
    ↓
得到一堆自动配置类（如 DataSourceAutoConfiguration）
    ↓
逐个用 @ConditionalOn... 判断是否生效
    ↓
生效的配置类注册对应的 Bean
    ↓
用户自己定义的 Bean 优先，自动配置退让


# Spring框架常见注解

Spring 都是些很常见的

SpringMVC 着重控制层细节的参数

Springboot自动配置 扫描包 实现配置文件 

