# Server基本知识


## Tomcat

---

Tomcat 是一个小型的轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选，因为Tomcat 技术先进、性能稳定，成为目前比较流行的Web 应用服务器。Tomcat是应用（java）服务器，它只是一个servlet容器，是Apache的扩展，但它是独立运行的。

对于一个初学者来说，可以这样认为，当在一台机器上配置好Apache 服务器，可利用它响应HTML（标准通用标记语言下的一个应用）页面的访问请求。实际上Tomcat 部分是Apache 服务器的扩展，但它是独立运行的，所以当你运行tomcat 时，它实际上作为一个与Apache 独立的进程单独运行的。

诀窍是，当配置正确时，Apache 为HTML页面服务，而Tomcat 实际上运行JSP 页面和Servlet。另外，Tomcat和IIS等Web服务器一样，具有处理HTML页面的功能，另外它还是一个Servlet和JSP容器，独立的Servlet容器是Tomcat的默认模式。不过，Tomcat处理静态HTML的能力不如Apache服务器。

### Tomcat的工作模式

Tomcat有3中工作模式：

1. 作为独立的Servlet容器，这是默认工作模式。此时Tomcat会作为独立的服务器，Servlet容器组件作为服务器的一部分存在
1. 作为其他web服务器进程内的Servlet容器，此时Tomcat分为web服务器插件和Servlet容器组件，web服务器插件在其他web服务器进程地址空间内启动一个Jav虚拟机运行Servlet容器组件

![其他web服务器进程内的Servlet容器](http://images.cnitblog.com/blog/489427/201303/08220947-5fb3aa8facab47daa7977014cdf6ec47.png)

1. 作为其他web服务器外的Servlet容器组件，此时Tomcat分为web服务器插件和Servlet容器组件，web服务器插件会在其他web服务器进程地址空间之外启动一个Java虚拟机运行Servlet容器组件


### Tomcat Server处理一个HTTP请求的过程

![Tomcat Server处理一个HTTP请求的过程](http://img1.tuicool.com/Mnqe22j.png!web)

1. 用户点击网页内容，请求被发送到本机端口8080，被在那里监听的Coyote HTTP/1.1 Connector获得。 
1. Connector把该请求交给它所在的Service的Engine来处理，并等待Engine的回应。 
1. Engine获得请求localhost/test/index.jsp，匹配所有的虚拟主机Host。 
1. Engine匹配到名为localhost的Host（即使匹配不到也把请求交给该Host处理，因为该Host被定义为该Engine的默认主机），名为localhost的Host获得请求/test/index.jsp，匹配它所拥有的所有的Context。Host匹配到路径为/test的Context（如果匹配不到就把该请求交给路径名为“ ”的Context去处理）。 
1. path=“/test”的Context获得请求/index.jsp，在它的mapping table中寻找出对应的Servlet。Context匹配到URL PATTERN为*.jsp的Servlet,对应于JspServlet类。 
1. 构造HttpServletRequest对象和HttpServletResponse对象，作为参数调用JspServlet的doGet（）或doPost（）.执行业务逻辑、数据存储等程序。 
1. Context把执行完之后的HttpServletResponse对象返回给Host。 
1. Host把HttpServletResponse对象返回给Engine。 
1. Engine把HttpServletResponse对象返回Connector。 
1. Connector把HttpServletResponse对象返回给客户Browser。



## Serlvet

---

Servlet（Server Applet），全称Java Servlet，暂无中文译文。是用Java编写的服务器端程序。其主要功能在于交互式地浏览和修改数据，生成动态Web内容。狭义的Servlet是指Java语言实现的一个接口(一个类)，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。

Servlet运行于支持Java的应用服务器中。从原理上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。

Servlet生命周期???

todo...XXX


[Servlet 简介](http://www.runoob.com/servlet/servlet-intro.html)

todo...XXX



## CDN

---

CDN的全称是Content Delivery Network，即内容分发网络。其基本思路是尽可能避开互联网上有可能影响数据传输速度和稳定性的瓶颈和环节，使内容传输的更快、更稳定。通过在网络各处放置节点服务器所构成的在现有的互联网基础之上的一层智能虚拟网络，CDN系统能够实时地根据网络流量和各节点的连接、负载状况以及到用户的距离和响应时间等综合信息将用户的请求重新导向离用户最近的服务节点上。其目的是使用户可就近取得所需内容，解决 Internet网络拥挤的状况，提高用户访问网站的响应速度。

关键功能:

- 内容发布：它借助于建立索引、缓存、流分裂、组播（Multicast）等技术，将内容发布或投递到距离用户最近的远程服务点处；
- 内容路由：它是整体性的网络负载均衡技术，通过内容路由器中的重定向（DNS）机制，在多个远程POP上均衡用户的请求，使得用户请求得到最快内容源的响应；
- 内容交换：它根据内容的可用性、服务器的可用性以及用户的背景，在POP的缓存服务器上，利用应用层交换、流量分类、重定向（ICP、WCCP）等技术，智能地平衡负载流量；
- 性能管理：它通过内部和外部监控系统，获取网络部件的状况信息，测量内容发布的端到端性能（如包丢失、延时、平均带宽、启动时间、帧速率等），保证网络处于最佳的运行状态。

CDN用户访问流程图如下:

![CDN用户访问流程图](http://img.blog.csdn.net/20130725150332968?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29vbG1lbWU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

具体步骤如下:

1. 用户向浏览器输入www.web.com这个域名，浏览器第一次发现本地没有dns缓存，则向网站的DNS服务器请求；
1. 网站的DNS域名解析器设置了CNAME，指向了www.web.51cdn.com,请求指向了CDN网络中的智能DNS负载均衡系统；
1. 智能DNS负载均衡系统解析域名，把对用户响应速度最快的IP节点返回给用户；
1. 用户向该IP节点（CDN服务器）发出请求；
1. 由于是第一次访问，CDN服务器会向原web站点请求，并缓存内容；
1. 请求结果发给用户。

当用户访问加入CDN服务的网站时，域名解析请求将最终交给全局负载均衡DNS进行处理。

对于普通的Internet用户来讲，每个CDN节点就相当于一个放置在它周围的WEB。通过全局负载均衡DNS的控制，用户的请求被透明地指向离他最近的节点，节点中CDN服务器会像网站的原始服务器一样，响应用户的请求。由于它离用户更近，因而响应时间必然更快。

每个CDN节点由两部分组成:负载均衡设备和高速缓存服务器.

CDN网络是在用户和服务器之间增加Cache层，如何将用户的请求引导到Cache上获得源服务器的数据，主要是通过接管DNS实现，这就是CDN的最基本的原理，当然很多细节没有涉及到，比如第1步，首先向本地的DNS服务器请求。第5步，内容淘汰机制（根据TTL）等。但原理大体如此。



详情可以看[一张图说明CDN网络的原理](http://blog.csdn.net/coolmeme/article/details/9468743) .

## Nginx

---

Nginx ("engine x")  ， Nginx ( “ engine x ” )  是俄罗斯人 Igor Sysoev( 塞索耶夫 ) 编写的一款高性能的  HTTP  和反向代理服务器。也是一个 IMAP/POP3/SMTP 代理服务器；也就是说， Nginx 本身就可以托管网站，进行 HTTP 服务处理，也可以作为反向代理服务器使用。

反向代理服务器：在服务器端接受客户端的请求，然后把请求分发给具体的服务器进行处理，然后再将服务器的响应结果反馈给客户端。 Nginx 就是其中的一种反向代理服务器软件。

具体查看[Nginx详解***](http://www.tuicool.com/articles/uABvY3).



## MQ

---

消息队列中间件是分布式系统中重要的组件，主要解决应用耦合，异步消息，流量削锋等问题。实现高性能，高可用，可伸缩和最终一致性架构。是大型分布式系统不可缺少的中间件。

目前在生产环境，使用较多的消息队列有ActiveMQ，RabbitMQ，ZeroMQ，Kafka，MetaMQ，RocketMQ等。

Message Queue（MQ），消息队列中间件。很多人都说：MQ通过将消息的发送和接收分离来实现应用程序的异步和解偶，这个给人的直觉是——MQ是异步的，用来解耦的，但是这个只是MQ的效果而不是目的。
　　
MQ真正的目的是为了通讯，屏蔽底层复杂的通讯协议，定义了一套应用层的、更加简单的通讯协议。


详情可以阅读[大型网站架构之分布式消息队列**](http://blog.csdn.net/shaobingj126/article/details/50585035) .



## Memcache:

---

### MemCache是什么?

MemCache是一个自由、源码开放、高性能、分布式的分布式内存对象缓存系统，用于动态Web应用以减轻数据库的负载。它通过在内存中缓存数据和对象来减少读取数据库的次数，从而提高了网站访问的速度。 可应用各种需要缓存的场景，其主要目的是通过降低对Database的访问来加速web应用程序。MemCaChe是一个存储键值对的HashMap，在内存中对任意的数据（比如字符串、对象等）所使用的key-value存储，数据可以来自数据库调用、API调用，或者页面渲染的结果。MemCache设计理念就是小而强大，它简单的设计促进了快速部署、易于开发并解决面对大规模的数据缓存的许多难题，而所开放的API使得MemCache能用于Java、C/C++/C#、Perl、Python、PHP、Ruby等大部分流行的程序语言。


### MemCache和MemCached的区别：

1. MemCache是项目的名称.
1. MemCached是MemCache服务器端可以执行文件的名称

MemCache访问模型:

![Memcache访问模型](http://img.ptcms.csdn.net/article/201603/16/56e8c992e136f_middle.jpg?_=31834)

特别澄清一个问题，MemCache虽然被称为”分布式缓存”，但是MemCache本身完全不具备分布式的功能，MemCache集群之间不会相互通信（与之形成对比的，比如JBoss Cache，某台服务器有缓存数据更新时，会通知集群中其他机器更新缓存或清除缓存数据），所谓的”分布式”，完全依赖于客户端程序的实现，就像上面这张图的流程一样。

同时基于这张图，理一下MemCache一次写缓存的流程：

1. 应用程序输入需要写缓存的数据
1. API将Key输入路由算法模块，路由算法根据Key和MemCache集群服务器列表得到一台服务器编号
1. 由服务器编号得到MemCache及其的ip地址和端口号
1. API调用通信模块和指定编号的服务器通信，将数据写入该服务器，完成一次分布式缓存的写操作

读缓存和写缓存一样，只要使用相同的路由算法和服务器列表，只要应用程序查询的是相同的Key，MemCache客户端总是访问相同的客户端去读取数据，只要服务器中还缓存着该数据，就能保证缓存命中。

为了提高性能，memcached中保存的数据都存储在memcached内置的内存存储空间中。由于数据仅存在于内存中，因此重启memcached、重启操作系统会导致全部数据消失。

详情可以参考[MemCache超详细解读 **](http://www.csdn.net/article/2016-03-16/2826609)



## Redis

---

Redis是一个key-value存储系统。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list(链表)、set(集合)和zset(有序集合)。这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。

Redis有两种存储方式，默认是snapshot方式，实现方法是定时将内存的快照(snapshot)持久化到硬盘，这种方法缺点是持久化之后如果出现crash则会丢失一段数据。因此在完美主义者的推动下作者增加了aof方式。aof即append only mode，在写入内存数据的同时将操作命令保存到日志文件，在一个并发更改上万的系统中，命令日志是一个非常庞大的数据，管理维护成本非常高，恢复重建时间会非常长，这样导致失去aof高可用性本意。

像MySQL一样，redis是支持主从同步的，而且也支持一主多从以及多级从结构。 主从结构，一是为了纯粹的冗余备份，二是为了提升读性能，比如很消耗性能的SORT就可以由从服务器来承担。

redis的主从同步是异步进行的，这意味着主从同步不会影响主逻辑，也不会降低redis的处理性能。 主从架构中，可以考虑关闭主服务器的数据持久化功能，只让从服务器进行持久化，这样可以提高主服务器的处理性能。


一些数据库和缓存服务器的特性与功能表如下:

名称|类型|数据存储选项| 查询类型 |附加功能
-|-|-|-|-
Redis| 使用内存存储（in-memory）的非关系数据库| 字符串、列表、集合、散列表、有序集合| 每种数据类型都有自己的专属命令，另外还有批量操作（bulk operation）和不完全（partial）的事务支持| 发布与订阅，主从复制（master/slave replication），持久化，脚本（存储过程，stored procedure）
memcached| 使用内存存储的键值缓存| 键值之间的映射| 创建命令、读取命令、更新命令、删除命令以及其他几个命令| 为提升性能而设的多线程服务器
MySQL| 关系数据库| 每个数据库可以包含多个表，每个表可以包含多个行；可以处理多个表的视图（view）；支持空间（spatial）和第三方扩展| SELECT、 INSERT、 UPDATE、 DELETE、函数、存储过程| 支持ACID性质（需要使用InnoDB），主从复制和主主复制 （master/master replication）
PostgreSQL| 关系数据库| 每个数据库可以包含多个表，每个表可以包含多个行；可以处理多个表的视图；支持空间和第三方扩展；支持可定制类型| SELECT、 INSERT、 UPDATE、 DELETE、内置函数、自定义的存储过程| 支持ACID性质，主从复制，由第三方支持的多主复制（multi-master replication）
MongoDB| 使用硬盘存储（on-disk）的非关系文档存储 | 每个数据库可以包含多个表，每个表可以包含多个无schema（schema-less）的BSON文档| 创建命令、读取命令、更新命令、删除命令、条件查询命令等| 支持map-reduce操作，主从复制，分片，空间索引（spatial index）



## mongodb

---

MongoDB是一个基于分布式文件存储的数据库。由C++语言编写。旨在为WEB应用提供可扩展的高性能数据存储解决方案。

MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。

Mongo最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引.

个人理解:  
由于mongodb采用类似Json的bson格式, 所以它的里面可以存储一对多的关系, 比如下面文档(相当于关系数据库中的行)存储的是一篇文章的信息, 它包含了多个评论和多个tags.

```
_id: POST_ID
	title: TITLE_OF_POST, 
	description: POST_DESCRIPTION,
	author: POST_BY,
	tags: [TAG1, TAG2, TAG3],
	likes: TOTAL_LIKES, 
	comments: [  
		{
			user:'COMMENT_BY',
			message: TEXT,
			dateCreated: DATE_TIME,
		},
		{
			user:'COMMENT_BY',
			message: TEXT,
			dateCreated: DATE_TIME,
		}
	]
```
**如果用关系数据库实现, 它创建评论的表, 创建tag相关的标, 查询是要跨表查询,速度较慢, 而使用mongodb, 直接使用一个集合(相当于关系数据库的表),在一个集合里查询就可以了. 这也是mongodb的一个优点.**


### 几个概念

1. 文档  
    文档时mongodb中数据的基本单元，类似关系型数据库中的行。对比:

    - 关系型数据库：行是标识一条存在数据库中的记录，行有唯一标识的字段，比如Oracle就有隐藏存在的rowid。行有列，标识对应字段的名称，字段值为列所表示的值。
    - Mongodb: 文档标识集合中的一条记录，即集合中的一个对象，形象的对比：数组中的一个元素，List中的一个元素等（个人理解）。文档有唯一的标识“_id”,数据库可自动生成，可类比oracle的rowid。 文档以key/value的方式,如下文档：{"name":"jack","age":20} 可类比数据表的列，以及列对应的值。

1. 集合  
    在mongodb中是一组文档，类似关系型数据库中的数据表。对比:

    - 关系型数据库：表是存储多个数据的，表中存在多行。表，即模式.表名。表中的数据行在列数、列的类型都是一样。
    - Mongodb: mongodb数据库不是关系型数据库，没有模式的概念。集合中的文档可以使不同形式的。比如下面可以存在同一个集合当中：

        ```
        {"name":"jack","age":19}
        {"name":"wangjun","age":22,"sex":"1"}
        ```

    跟关系型数据库的数据表、组数、列表对比看，我觉得mongodb的集合更像列表List.

1. 数据库  
  mongodb中多个文档构成集合，多个集合构成数据库。对比:

    - 关系型数据库: 在安装数据库的时候数据库实例创建，同时存在系统默认的管理员用户。之后可以创建多个用户并进行赋权，创建的表存在于不同的用户之下，不同的用户存储着不同的数据。
    - Mongodb: mongodb以文档的形式保存在集合中，可以同一数据库存储不同的数据或者集合，即DB2、oracle、teradata等都可以存储在同一个数据库中。最近做的项目就可以将这三者数据库的数据都保存到同一数据库中。

    保留数据库名：admin、local、config.


### mongodb缺点

1. 不支持事务操作
1. 占用空间过大
1. MongoDB没有如MySQL那样成熟的维护工具
1. 大数据量持续插入，写入性能有较大波动
1. 无法进行关联表查询，不适用于关系多的数据
1. 复杂聚合操作通过mapreduce创建，速度慢
1. 模式自由,自由灵活的文件存储格式带来的数据错误



## MySQL

---

MySQL是一个小型关系型数据库管理系统，开发者为瑞典MySQL AB公司，现在已经被Sun公司收购，支持FreeBSD、Linux、MAC、Windows等多种操作系统与其他的大型数据库例如Oracle、DB2、SQL Server等相比功能稍弱一些:

1. 可以处理拥有上千万条记录的大型数据
1. 支持常见的SQL语句规范
1. 可移植行高，安装简单小巧
1. 良好的运行效率，有丰富信息的网络支持
1. 调试、管理，优化简单(相对其他大型数据库)

MySQL是由原MySQL AB公司自主研发的，是目前IT行业最流行的开放源代码的数据库管理系统，同时它也是一个支持多线程高并发多用户的关系型数据库管理系统。性能高一直是MySQL引以自豪的一个特点。

总体来说，MySQL数据库在发展过程中一直追求三项原则：简单、高效、可靠。从上面简单的比较重也可以看出，MySQL在这三项原则上面，没有哪一项是做的不好的。而且，虽然功能并不是MySQL自身追求的原则之一，但是考虑到当前用户量急剧增长，用户需求越来越多样化，MySQL也不得不在功能方面做出大量的努力，以不断满足客户的新需求。

MySQL数据库服务器的master-slave模式，利用数据库服务器在主从服务器间进行同步，应用只把数据写到主服务器，而读数据时则根据负载选择一台从服务器或者主服务器来读取，将数据按不同策略划分到不同的服务器（组）上，分散数据库压力。

** MySQL Proxy做MySQL服务器集群的负载均衡并实现读写分离。其实现读写分离的基本原理是让主数据库处理事务性查询，而从数据库处理SELECT查询。数据库复制被用来把事务性查询导致的变更同步到集群中的从数据库。 **


## 数据库系统

---

todo...XXX



## 网关服务

---

网关服务是单一访问点，并充当多项服务的代理。服务网关启用了跨所有服务的变换、路由和公共处理。

服务网关模块是单一调解，用于处理对多个服务使用者和提供者的请求。任何服务网关都有如下四个典型步骤：

1. 常用处理 - 一旦网关接收到消息，就对所有消息执行常用处理，例如添加协议级的头或者记录该消息。
1. 服务标识 - 必须将网关所处理的消息标识为特定服务类型。例如，查询消息以确定它是针对服务提供者 A、B 还是 C。
1. 端点路由 - 当它确定某消息将传递到特定服务提供者时，它将映射到网络可寻址端点，以便可以将该消息转发到服务提供者。
1. 特定于服务的处理 - 执行特定目标服务所需的任何处理。

用户可以根据不同的场景更改这四个步骤的顺序。[1] 

为了更好的理解它, 可以参考[服务端架构中的“网关服务器” **](http://blog.csdn.net/wallwind/article/details/41121877).

网关服务器的作用应该是：

1. 聚合客户的不同业务。客户端只需连接一个网关，不同业务由网关分发到不同的功能服务器。如果功能分得极细，如组队功能由服务器A处理，装备升级由B处理，C, D等。客户端不应该直接连接A,B,C,D等，有网关转发就简单了。
2. 聚合客户端的连接。内部逻辑服务器的数量应该会大于网关数量。一个网关可能连接1w人，而地图服务器只能承载1k人， 所以暴露10个逻辑服务器不如仅暴露1个网关，可以少占用外网IP。顺便避免了客户端切换地图的断开重连。


## zuul

---

Zuul 是 Netflix 的网关系统，提供了动态路由、监控、安全控制等功能。Zuul 是开源的（https://github.com/Netflix/zuul），除了 Netflix，Spring Cloud 和 JHipster 等项目也用到了它。

todo...XXX



## 负载均衡

---

负载均衡（Load Balance）是分布式系统架构设计中必须考虑的因素之一，它通常是指，将请求/数据【均匀】分摊到多个操作单元上执行，负载均衡的关键在于【均匀】。

负载均衡是一种技术，指通过某种算法实现负载分担的方法。通俗的讲就是统一分配请求的设备，负载均衡会统一接收全部请求，然后按照设定好的算法将这些请求分配给这个负载均衡组中的所有成员，以此来实现请求（负载）的均衡分配。

常见互联网分布式架构如下，分为客户端层、反向代理nginx层、站点层、服务层、数据层。可以看到，每一个下游都有多个上游调用，只需要做到，每一个上游都均匀访问每一个下游，就能实现“将请求/数据【均匀】分摊到多个操作单元上执行”。

常见的负载均衡方案如下:

![负载均衡方案](https://static.oschina.net/uploads/space/2016/0916/072804_kJyJ_2903254.jpg)



负载均衡系统分为硬件和软件两种。硬件负载均衡效率高，但是价格贵，比如F5等。软件负载均衡系统价格较低或者免费，效率较硬件负载均衡系统低，不过对于流量一般或稍大些网站来讲也足够使用，比如lvs/nginx/haproxy。大多数网站都是硬件、软件负载均衡系统并用。

一般对负载均衡的使用是随着网站规模的提升根据不同的阶段来使用不同的技术。具体的应用需求还得具体分析，如果是中小型的Web应用，比如日PV小于1000万，用Nginx就完全可以了；如果机器不少，可以用DNS轮询，LVS所耗费的机器还是比较多的；大型网站或重要的服务，且服务器比较多时，可以考虑用LVS。

目前关于网站架构一般比较合理流行的架构方案：Web前端采用Nginx/HAProxy+Keepalived作负载均衡器；后端采用MySQL数据库一主多从和读写分离，采用LVS+Keepalived的架构。当然要根据项目具体需求制定方案。

可以看下[一分钟了解负载均衡的一切](http://www.oschina.net/news/77156/load-balance), 加深理解.


### Keepalived

keepalived是一个类似于layer3, 4 & 7交换机制的软件，也就是我们平时说的第3层、第4层和第7层交换。

Keepalived的作用是检测服务器的状态，如果有一台web服务器死机，或工作出现故障，Keepalived将检测到，并将有故障的服务器从系统中剔除，同时使用其他服务器代替该服务器的工作，当服务器工作正常后Keepalived自动将服务器加入到服务器群中，这些工作全部自动完成，不需要人工干涉，需要人工做的只是修复故障的服务器。

在layer3网络层上, Keepalived会定期向服务器群中的服务器发送一个ICMP的数据包（既我们平时用的Ping程序).



## 分布式存储系统

---

xx


## 文件存储

---



## 代码发布系统

---

xx



---

1. Lamp
1. 集群节点

1. 负载均衡技术

1. allway sync  
    Allway Sync是一个非常容易使用的 Windows 文件同步软件。 它可以在几个文件夹之间进行文件同步，自动将更新的文件覆盖几个同步文件夹中的旧文件。软件带有一个小型数据库，监视每次更新后的文件状态。如果一次同步之后，你删除了同步文件夹中某些文件，它在同步的时候将其它的几个文件夹的副本也删除，而不会将未删除的旧文件重复拷贝到更新的文件夹。

    补充：Allway Sync并不是一个绝对的免费软件，根据运行的目录数、文件数，软件本身会作出判断是否要求用户购买收费的高级版本。



## Question

---

1. MemCache的服务器集群除了在内存中存放缓存,这个服务器还会用来干别的吗? 即这个服务器除了当做memcache的服务器,还会同时做它用吗?
1. 什么数据要放到Memcache里? memcache除了存放在memecache的机器上, 在用到memcache的客户端会cache吗?
1. 秒杀?
1. 消息队列除了一边存一边取, 我们现在中间有没有做什么处理?
1. A1服务器上需要的东西在用到时候去C1去获取? 会不会很慢? 这时候有缓存了?
1. 数据放到一台机器上, 同类的其他机器上需不需要同步的?
1. stone 网关服务现在都怎么工作的? zuul? 怎么转发? 发什么?
1. 直接本地获取和通过网络获取差多少时间??
1. 数据库主从:

    - 读数据和写数据库是不是分开的?, 
    - 写是不是都在主上做的? 主只有一个? 都在主上更新?如果是, 数据库上的负载均衡是在从上做吗?
    - 平常服务器的写操作, 都是从一个服务器上发出的吗?  不是会跑很多相同能的进程吗?
    - 多个地方写, 是在一个主上? 
    - 写了马上会同步到从服务器吗?如果这时候访问从呢?
    - MySQL数据库服务器的master-slave模式，利用数据库服务器在主从服务器间进行同步，应用只把数据写到主服务器，而读数据时则根据负载选择一台从服务器或者主服务器来读取，将数据按不同策略划分到不同的服务器（组）上，分散数据库压力。 这个工作谁做的? 负载均衡?




...
1. 共享, 同步.


## Reference

---

1. [一个可供创业公司参考的移动APP服务端架构演进方案](http://www.infoq.com/cn/articles/an-evolution-scheme-for-mobile-app-server-architecture)
1. [大型网站图片服务器架构的演进](http://blog.csdn.net/dinglang_2009/article/details/31450731)
1. [Nginx详解***](http://www.tuicool.com/articles/uABvY3)
1. [MemCache超详细解读 **](http://www.csdn.net/article/2016-03-16/2826609)
1. [Memcache 详解 **](http://freeloda.blog.51cto.com/2033581/1289806/)
1. [redis缓存技术学习](http://www.iigrowing.cn/redis-huan-cun-ji-shu-xue-xi.html)
1. [超强、超详细Redis数据库入门教程](http://www.jb51.net/article/56448.htm)
1. [学习Redis从这里开始**](http://www.epubit.com.cn/article/200)
1. [Memcached 与 Redis 实现的对比 **](http://blog.jobbole.com/108080/)
1. [大话消息队列的流派之争](http://udn.yyuap.com/thread-133421-1-1.html)
1. [分布式开放消息系统(RocketMQ)的原理与实践 **](http://www.jianshu.com/p/453c6e7ff81c)
1. [消息队列应用场景](http://www.cnblogs.com/stopfalling/p/5375492.html)
1. [使用消息队列的 10 个理由](https://www.oschina.net/translate/top-10-uses-for-message-queue)
1. [大型网站架构之分布式消息队列**](http://blog.csdn.net/shaobingj126/article/details/50585035)
1. [MongoDB 极简实践入门**](http://www.tuicool.com/articles/YzAfAbY)
1. [Zuul：Netflix的云网关系统](http://www.qingpingshan.com/rjbc/yunjisuan/151864.html)
1. [服务端架构中的“网关服务器” **](http://blog.csdn.net/wallwind/article/details/41121877)
1. [一分钟了解负载均衡的一切***](http://www.oschina.net/news/77156/load-balance)
1. [Nginx/LVS/HAProxy负载均衡软件的优缺点详解**](http://www.ha97.com/5646.html)
1. [为什么数据库读写分离可以提高性能](https://my.oschina.net/candiesyangyang/blog/203425)
1. [Servlet 简介*](http://www.runoob.com/servlet/servlet-intro.html)