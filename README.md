# java-interview
一些面试方面的知识点吧

#### 三层结构：
  
    数据持久层：主要就是数据库操作，JDBC 、`hibernate、 mybatis
    业务逻辑层：Servlet是最基本的，框架技术Struts 、 SpringMVC 什么的
    表示层：就是展示给用户看的那些网页和界面，常见的就是jsp和html

ORM：对象关系映射  CRM：客户关系管理

Hibernate和Mybatis：
都是持久层框架，对数据库存进行访问和操作。
区别：Hibernate对JDBC进行了深层次的封装，可移植性好(因为强大的映射结构和hql语言)
	Mybatis:移植性不如hibernate,但sql语句的直接优化上要方便，<br>hibernate很多sql语句是自动化成的，mybatis是通过xml配置文件

StringBuffer属于线程安全，相对为重量级(多线程时优先使用)
StringBuilder属于非线程安全，相对为轻量级(单线程时优先使用)
	可以动态地构造字符串，方便进行字符串的修改，String是不可变字符串，重新赋值其实是两个对象
它两方法差不多：
```
StringBuffer s = new StringBuffer();
StringBuffer sb = new StringBuffer(“abc”);
sb.append(“abc);
sb. deleteCharAt(1);
sb. delete (1,4);     [1,4)
sb.insert(4,false);
sb.setCharAt(1,’D’);
```
#### JSP内置对象：
```
pageContext, request, session, application, response, out, config, exception, page
```
Log4j四个级别，优先级从高到低分别是 ERROR、WARN、INFO、DEBUG
Log4j由三个重要的组件构成: 	优先级,输出目的地，输出格式

原生Mybatis
```
String resource = "mybatisConfig.xml";
		InputStream inputStream = Resources.getResourceAsStream(resource);
		SqlSessionFactory ssf = new SqlSessionFactoryBuilder().build(inputStream);
		SqlSession session = ssf.openSession();
		
		session.insert("test.insert",new Bank(7,1007,"钱七",6600));    //插入
		session.commit();                    //提交
		session.close();
```



队列和栈：
队列：先进先出，一端插入，另一端删除
栈:先进后出，同一端插入和删除
```
struts2和springMVC
struts2框架是类级别的拦截，每次来了请求就创建一个Action，然后调用setter getter方法把request中的数据注入
struts2实际上是通过setter getter方法与request打交道的 
struts2中，一个Action对象对应一个request上下文
```
spring3 mvc不同，spring3mvc是方法级别的拦截，拦截到方法后根据参数上的注解，把request数据注入进去
在spring3mvc中，一个方法对应一个request上下文 
所以说从架构本身上 spring3 mvc就容易实现restful url 

#### Oracle语句优化：
```
1．正确的建立的有效的索引
2．避免让索引列成为函数一部分，比如在索引列上使用计算。
3．避免在索引列上使用IS NULL和IS NOT NULL 
4．如果语句能够避免子查询，就尽量不用子查询。因为子查询的开销是相当昂贵的
5．在查询中尽量不使用“*”，去掉不需要的字段
6．指定查询范围时多使用IN，可代替 or
低效:SELECT … FROM DEPT WHERE SAL * 12 > 25000;
高效:SELECT … FROM DEPT WHERE SAL > 25000/12;
低效:(索引失效) SELECT … FROM DEPARTMENT WHERE DEPT_CODE IS NOT NULL;
```
#### 在什么情况下索引失效：
     1、索引列过滤数据的量太大可能会失效 2，联合索引-导引列没使用也会失效 3，索引字段被包含在函数体内可能会失效

#### 跳转页面有什么形式
```
   get是从服务器上获取数据，post是向服务器传送数据
   两种的区别：
   1) get是从服务器上获取数据，post是向服务器传送数据。
   2) get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
   3) 对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据。
   4) get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB
   5)get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；```
```

#### 系统性能通过哪几方面优化
```
首先是从三方面来提高的，应用层面，服务器端层面，数据库层面。
   一、应用层面
      采用freemaker或者velocity来做页面静态化，提高网站的访问速度。
   二、服务器端(记几种就可以了)
       1、对于一些不经常增删改的数据做缓存，比如memcached，redis，mongodb 
       2、对于安全方面，采用数据库事务来保证数据的安全性能。
       3、能尽量少的使用锁来处理，因为锁有时候会带来一系列的连锁反应。
       4、数据的一致性问题，需要考虑java concurrent包
       5、适当的使用一些高效算法。
       6、JVM的内存模型以及JVM的垃圾回收机制，一直垃圾回收器的合理使用，新生代和老年代的合理分区。  
   三、数据库层面(记几种就可以了)
       1、给数据库字段做索引，能够加快查询速度，不是所有的索引都能够加快查询速度的，前提是对于查询多于增删改的数据。
       2、给数据库表做表分区，能够加速查询的速度。 
       4、根据explain命令对于sql语句进行解释执行计划分析。
       5、对表进行分区，分区查询会加快速度的
       6、oracle的话。需要选择合适的选择器，根据实际需要，选择基于成本的选择器，或者基于基于规则的优化器
       7、in和exists，还有not in和not exists的用法区别，以及适用场合
```

#### 需要了解MVC模式/SSH框架(记主要的几种就可以了)
    SPRING七大模块的了解：
         * 核心容器(Spring core)、
         * Spring上下文(Spring context)、
         * Spring面向切面编程(Spring AOP)
         * Spring DAO模块、
         * Spring ORM模块
         * Spring Web模块、
         * Spring MVC框架(Spring WebMVC)

##### Ioc（控制反转）：
    把 javabean中的依赖关系交给一个控制中心(spring ioc容器)进行统一分配注入。所以ioc我们也可以把它称为依赖注入di（dependency injection）
##### AOP（面向方面编程Aspect-Oriented Programming）：
    可以说是OOP(面向对象编程)的补充和完善.
    横切代码(cross-cutting): 散布在各处的无关的代码。如日志，安全性、异常处理和透明的持续性。
##### Aspect(方面)：
    将那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，减少重复代码，降低模块间的耦合度， AOP代表的是一个横向的关系（横切技术）

#### 系统见接口如果调用传参
```
   1，根据双方协定的接口文档及字段顺序进行数据传递
   2，数据交互形式：标准的XMl文件、大字符串截取
   3，系统间交互实现：socket、webservice等
```



#### springMVC原理：
```
主要由DispatcherServlet、处理器映射、处理器、视图解析器、视图组成
1.	DispatcherServlet接收到一个HTTP请求，根据对应配置文件中的处理机映射，找到处理器（Handler）
2.	2.调用Handler中的方法，处理该请求，处理完后返回一个ModelAndView类型的数据给DispatcherServlet
3.	3.DispatcherServlet根据得到的ModelAndView中的视图对象，找到一个合适的ViewResolver（视图解析器），根据视图解析器的配置，DispatcherServlet将视图要显示的数据传给对应的视图，最后给浏览器构造一个HTTP响应。

DispatcherServlet是整个Spring MVC的核心。它负责接收HTTP请求组织协调Spring MVC的各个组成部分。其主要工作有以下三项：
1）截获符合特定格式的URL请求。
2）初始化DispatcherServlet上下文对应的WebApplicationContext，并将其与业务层、持久化层的WebApplicationContext建立关联。
3）初始化Spring MVC的各个组成组件，并装配到DispatcherServlet中
```
空指针异常的处理：
调用对象之前，进行非空验证

### 异常：两类
Error错误，是不可挽回的，也就是说，出了Error程序就挂了，最常见的就是OutOfMemoryError。
Exception：编译时异常指的是我们必须在代码中显示的处理，或者try或者throw，处理完成后才能编译成功，常见的是IOException。
RuntimeException：运行期异常指的是我们写的代码可以编译通过，但是如果运行时出现问题，则会出现运行期异常，最常见的就是NullPointerException、IndexOutOfBoundsException

线程:是指进程内的一个执行单元,也是进程内的可调度实体.
与进程的区别:
(1)地址空间:进程内的一个执行单元;进程至少有一个线程;它们共享进程的地址空间;而进程有自己独立的地址空间;
(2)资源拥有:进程是资源分配和拥有的单位,同一个进程内的线程共享进程的资源
(3)线程是处理器调度的基本单位,但进程不是.
4)二者均可并发执行. 


定位死循环linux：
先用top命令找到占用CPU最大的进程，记下进程pid

然后查看这个进程下哪个线程占用的资源最多 top -Hp 12862
比如看到pid为 12907的线程，把pid转化为16进制，为 326b

用 jstack -l 12862 > jstack.log； 生成线程堆栈日志文件

打开jstack.log文件  搜索0x326b，定位到死循环的代码块,





#### OutOfMemoryError常见的原因：
```
1.内存中加载的数据量过于庞大，如一次从数据库取出过多数据；
2.集合类中有对对象的引用，使用完后未清空，使得JVM不能回收；
3.代码中存在死循环或循环产生过多重复的对象实体；
4.使用的第三方软件中的BUG；
5.启动参数内存值设定的过小；
```
#### java内存划分：
```
栈内存：stack基本类型的变量和对象的引用。运行到作用域之外时自动释放。
堆内存：heap由 new 创建的对象和数组。没有引用指向它时，被标记为垃圾，在系统空闲时回收。
			Java虚拟机所管理的内存中最大的一块.
静态区：存放全局变量，静态变量和字符串常量，不释放
代码区：存放程序中方法的二进制代码，而且是多个对象共享一个代码空间区域
```
#### JVM垃圾回收机制：
    Java的垃圾回收机制是Java虚拟机提供的能力，用于在空闲时间以不定时的方式动态回收无任何引用的对象占据的内存空间，不是对象本身。System.gc()，Runtime.getRuntime().gc()  
显式通知JVM可以进行一次垃圾回收，但具体在什么时间点开始是不可预料的。

#### Java堆中各代分布:
```
Young新生代：主要是用来存放新生的对象。
Old老年代： 主要存放应用程序中生命周期长的内存对象。
Permanent永久区：主要存放Class和Meta的信息,Class在被 Load的时候被放入该区域. GC不会在主程序运行期对PermGen进行清理；
新生代频繁收集，老年较少收集，永久区基本不收集。
```
GC（或Minor GC）： 收集生命周期短的区域(Young area)。
Full GC（或Major GC）：收集Young area和Old area，对整个堆进行垃圾收集。

#### GC日志：
```
2012-11-15T16:57:12.524+0800: 8.490: [GC 8.490: [ParNew: 118016K->11244K(118016K), 0.0525525 secs] 183413K->83007K(511232K), 0.0527229 secs] [Times: user=0.08 sys=0.00, real=0.05 secs]
8.490 ：表示虚拟机启动运行到8.490秒是进行了一次monor Gc ( not Full GC)
ParNew :表示对年轻代进行的GC，使用ParNew 收集器
118016K->11244K(118016K) ：年轻代收集前大小，收集后大小，当前年轻代分配总大小
0.0525525 secs ：用户线程暂停的时间，即此次年轻代收集花费的时间
183413K->83007K(511232K) :JVM heap堆收集前后heap堆内存的变化
0.0527229 secs ：整个JVM此次垃圾造成用户线程的暂停时间。
```
#### 什么时候触发Full gc:
```
1. 老年代空间不足。旧生代空间只有在新生代对象转入及创建为大对象、大数组时才会出现不足。 
2. Permanet Generation空间满。系统中要加载的类、反射的类和调用的方法较多时
```

####  java多线程:
通过线程轮流切换并分配处理器执行时间的方式来实现的，在任何一个确定的时刻，一个处理器（对于多核处理器来说是一个内核）只会执行一条线程中的指令。因此，为了线程切换后能恢复到正确的执行位置，每条线程都需要有一个独立的程序计数器，各条线程之间的计数器互不影响，独立存储，我们称这类内存区域为“线程私有”的内存。

RMI：RMI:远程方法调用(Remote Method Invocation)。能够让在某个Java虚拟机上的对象像调用本地对象一样调用另一个java 虚拟机中的对象上的方法。(Remote接口，服务器客户端模式)

所传递的对象必须要实现 Serializable接口，基于序列化原理。

RMI：在tcp协议上传递可序列化java对象，只能用在java虚拟机上。服务器和客户端都java写。
webservice：是在http协议上传递xml文本文件，与语言和平台无关

ArrayList不是线程安全的，而Vector是线程安全的

#### http 错误代码表
```
所有 HTTP 状态代码及其定义。 
　代码  指示  
2xx  成功  
200  正常；请求已完成。  
201  正常；紧接 POST 命令。  
202  正常；已接受用于处理，但处理尚未完成。  
203  正常；部分信息 — 返回的信息只是一部分。  
204  正常；无响应 — 已接收请求，但不存在要回送的信息。  
3xx  重定向  
301  已移动 — 请求的数据具有新的位置且更改是永久的。  
302  已找到 — 请求的数据临时具有不同 URI。  
303  请参阅其它 — 可在另一 URI 下找到对请求的响应，且应使用 GET 方法检索此响应。  
304  未修改 — 未按预期修改文档。  
305  使用代理 — 必须通过位置字段中提供的代理来访问请求的资源。  
306  未使用 — 不再使用；保留此代码以便将来使用。  
4xx  客户机中出现的错误  
400  错误请求 — 请求中有语法问题，或不能满足请求。  
401  未授权 — 未授权客户机访问数据。  
402  需要付款 — 表示计费系统已有效。  
403  禁止 — 即使有授权也不需要访问。  
404  找不到 — 服务器找不到给定的资源；文档不存在。  
407  代理认证请求 — 客户机首先必须使用代理认证自身。  
415  介质类型不受支持 — 服务器拒绝服务请求，因为不支持请求实体的格式。  
5xx  服务器中出现的错误  
500  内部错误 — 因为意外情况，服务器不能完成请求。  
501  未执行 — 服务器不支持请求的工具。  
502  错误网关 — 服务器接收到来自上游服务器的无效响应。  
503  无法获得服务 — 由于临时过载或维护，服务器无法处理请求。
```

#### 1.从地址栏显示来说
* forward是服务器请求资源,服务器直接访问目标地址的URL,把那个URL的响应内容读取过来,然后把这些内容再发给浏览器.浏览器根本不知道服务器发送的内容从哪里来的,所以它的地址栏还是原来的地址.
* redirect是服务端根据逻辑,发送一个状态码,告诉浏览器重新去请求那个地址.所以地址栏显示的是新的URL.

#### 2.从数据共享来说
* forward:转发页面和转发到的页面可以共享request里面的数据.
* redirect:不能共享数据.

#### 3.从运用地方来说
* forward:一般用于用户登陆的时候,根据角色转发到相应的模块.
* redirect:一般用于用户注销登陆时返回主页面和跳转到其它的网站等.

#### 4.从效率来说
* forward:高.
* redirect:低.

spring Transaction中有一个很重要的属性：Propagation。主要用来配置当前需要执行的方法，与当前是否有transaction之间的关系。

我晓得有点儿抽象，这也是为什么我想要写这篇博客的原因。看了后面的例子，大家应该就明白了。


### 一、Propagation取值：
```
REQUIRED（默认值）：在有transaction状态下执行；如当前没有transaction，则创建新的transaction；

SUPPORTS：如当前有transaction，则在transaction状态下执行；如果当前没有transaction，在无transaction状态下执行；

MANDATORY：必须在有transaction状态下执行，如果当前没有transaction，则抛出异常IllegalTransactionStateException；

REQUIRES_NEW：创建新的transaction并执行；如果当前已有transaction，则将当前transaction挂起；

NOT_SUPPORTED：在无transaction状态下执行；如果当前已有transaction，则将当前transaction挂起；

NEVER：在无transaction状态下执行；如果当前已有transaction，则抛出异常IllegalTransactionStateException。
```
#### XML解析：  DOM和SAX是底层接口实现方式，JDOM和DOM4J是高层次的封闭库。

```
        常用DOM4J，性能最优。
DOM和SAX的不同：
     1. DOM是基于内存的，不管文件有多大，都会将所有的内容预先装载到内存中。从而消耗很大的内存空间。而SAX是基于事件的。当某个事件被触发时，才获取相应的XML的部分数据，从而不管XML文件有多大，都只占用了少量的内存空间。
     2. DOM可以读取XML也可以向XML文件中插入数据，而SAX却只能对XML进行读取，而不能在文件中插入数据。这也是SAX的一个缺点。
     3.SAX的另一个缺点：DOM我们可以指定要访问的元素进行随机访问，而SAX则不行。SAX是从文档开始执行遍历的。并且只能遍历一次。也就是说我们不能随机的访问XML文件，只能从头到尾的将XML文件遍历一次（当然也可以中间截断遍历）
```

#### Spring Controller读取参数：
```
url中的参数(get和post都可以在url中带参数),或者通过 Content-Type 为 application/x-www-form-urlencoded 的POST方式提交的参数：
	只能通过req.getParameter("name") 或@RequestParam的方法取到，无法在req.getInputStream()或req.getReader()的流中取到。
Content-Type为application/json的POST提交的参数：
	用req.getInputStream()或req.getReader()的流来取，或者用 @RequestBody注解来映射到实体类对象中。并且两种方式不能同时使用。
	无法用req.getParameter()来获取。

@RequestBody 也可以映射到Map对象，用法： @RequestBody Map<String, Object> map
@RequestParam 也可以把所有参数映射到Map，用法： @RequestParam Map<String, Object> map
```


 #### 1. String是一个对象。
    因为对象的默认值是null，所以String的默认值也是null；但它又是一种特殊的对象，有其它对象没有的一些特性。

 #### 2. new String()和new String(“”)都是申明一个新的空字符串，是空串不是null；
```
  3. String str=”kvill”；
   String str=new String (“kvill”);的区别：
  在这里，我们不谈堆，也不谈栈，只先简单引入常量池这个简单的概念。
  常量池(constant pool)指的是在编译期被确定，并被保存在已编译的.class文件中的一些数据。它包括了关于类、方法、接口等中的常量，也包括字符串常量。
  看例1：
  String s0=”kvill”;
  String s1=”kvill”;
  String s2=”kv” + “ill”;
  System.out.println( s0==s1 );
  System.out.println( s0==s2 );
  结果为：
  true
  true
  首先，我们要知结果为道Java会确保一个字符串常量只有一个拷贝。
  因为例子中的s0和s1中的”kvill”都是字符串常量，它们在编译期就被确定了，所以s0==s1为true；而”kv”和”ill”也都是字符串常量，当一个字符串由多个字符串常量连接而成时，它自己肯定也是字符串常量，所以s2也同样在编译期就被解析为一个字符串常量，所以s2也是常量池中”kvill”的一个引用。

  所以我们得出s0==s1==s2;

  用new String() 创建的字符串不是常量，不能在编译期就确定，所以new String() 创建的字符串不放入常量池中，它们有自己的地址空间。

  看例2：

  String s0=”kvill”;

  String s1=new String(”kvill”);

  String s2=”kv” + new String(“ill”);

  System.out.println( s0==s1 );

  System.out.println( s0==s2 );

  System.out.println( s1==s2 );

  结果为：

  false

  false

  false

  例2中s0还是常量池中”kvill”的应用，s1因为无法在编译期确定，所以是运行时创建的新对象”kvill”的引用，s2因为有后半部分new String(“ill”)所以也无法在编译期确定，所以也是一个新创建对象”kvill”的应用;明白了这些也就知道为何得出此结果了。
```

### 一．系统吞度量要素：
```

  一个系统的吞度量（承压能力）与request对CPU的消耗、外部接口、IO等等紧密关联。

单个reqeust 对CPU消耗越高，外部系统接口、IO影响速度越慢，系统吞吐能力越低，反之越高。

系统吞吐量几个重要参数：QPS（TPS）、并发数、响应时间

        QPS（TPS）：每秒钟request/事务 数量

        并发数： 系统同时处理的request/事务数

        响应时间：  一般取平均响应时间

（很多人经常会把并发数和TPS理解混淆）

理解了上面三个要素的意义之后，就能推算出它们之间的关系：

QPS（TPS）= 并发数/平均响应时间
```

