# **一**、JAVA基础

## 基础知识 

#### 基本数据类型

int、byte、short、long、boolean、float、double、char

| 基本类型 | 位数 | 字节 | 默认值 | 范围            |
| -------- | ---- | ---- | ------ | --------------- |
| byte     | 8    | 1    | 0      | -128-127        |
| short    | 16   | 2    | 0      | -2^15- 2^15 - 1 |
| int      | 32   | 4    | 0      | -2^31- 2^31 - 1 |
| long     | 64   | 8    | 0L     | -2^63- 2^63 - 1 |
| char     | 16   | 2    | u0000  | 0 - 2^16-1      |
| float    | 32   | 4    | 0f     | -2^31 - 2^31-1  |
| double   | 64   | 8    | 0d     | -2^63 - 2^63-1  |
| boolean  | 1    |      | false  |                 |

#### 关键字

**transient**将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会被序列化。

**assert**断言

**yield**应该做的是让当前运行线程回到可运行状态，Thread类提供的一个静态的方法，让当前正在执行的线程暂停，让出cpu资源给其他的线程，但是和sleep方法不同的是，它不会进入阻塞状态而是进入就绪状态。

#### Object类的常见方法总结

Object类是一个特殊的类，是所有类的父类。它主要提供了以下11个方法：

public final native Class<?> **getClass**()//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。 

public native int **hashCode**() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。

public boolean **equals**(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。 

protected native Object **clone**() throws CloneNotSupportedException//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。 

public String **toString**()//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。

public final native void **notify**()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。 

public final native void **notifyAll**()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。 

public final native void **wait**(**long** timeout) throws InterruptedException//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。 

public final void **wait**(long timeout, int nanos) throws InterruptedException//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。 

public final void **wait**() throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念 

protected void **finalize**() throws Throwable { }//实例被垃圾回收器回收的时候触发的操作

问完上面这个问题之后，面试官很可能紧接着就会问你“hashCode与equals”相关的问题。

#### 反射方式

1. Class.forName(String className)
2. className.class
3. 实例对象.getClass()

#### 排序算法

速度: **快速排序>>归并排序>>>>>插入排序>>选择排序>>冒泡排序**

**快速排序** 就是设置一个标准值, 将大于这个值的放到右边(不管排序), 将小于这个值的放到左边(不管排序), 那么这样只是区分了左小右大, 没有排序, 没关系, 左右两边再重复这个步骤.直到不能分了为止

**插入排序**将待插元素，依次与已排序好的子数列元素从后到前进行比较，如果当前元素值比待插元素值大，则将移位到与其相邻的后一个位置，否则直接将待插元素插入当前元素相邻的后一位置，因为说明已经找到插入点的最终位置

**冒泡排序**双重循环，找出最大的数放到最后

**选择排序**首先在未排序数列中找到最小元素，然后将其与数列的首部元素进行交换，然后，在剩余未排序元素中继续找出最小元素，将其与已排序数列的末尾位置元素交换。以此类推，直至所有元素圴排序完毕

**归并排序**

<img src="https://img-blog.csdnimg.cn/20190414142938622.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6emdkXzY2Ng==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom: 33%;" />

#### 重写与重载的区别

 重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理 

 重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法 

#### 静态变量、局部变量与成员变量的区别

- **静态变量**：静态变量属于类，所以也称为为类变量，随着类的加载而加载，随着类的消失而消失。存储于方法区的静态区。可以通过类名调用，也可以通过对象调用
- **局部变量**：方法内或方法声明上的变量，随着方法的调用而存在，随着方法的调用完毕而消失。存储于栈内存。只能通过对象名调用
- **成员变量**：类中方法外的变量，随着对象的存在而存在，随着对象的消失而消失。存储于堆内存。

#### 封装、继承、多态

#### final

#### ==与equals的区别

 **==** : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)。

**equals()** : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：

- 情况 1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。
- 情况 2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

#### hashCode()与 equals()

 `hashCode()` 的作用是获取哈希码，也称为散列码 

`hashCode`方法本质就是一个哈希函数，**将对象的地址值映为`integer`类型的哈希值。**

**为什么重写`equals`方法就得重写`hashCode`方法**

hashcode是用于散列数据的快速存取，如利用hash结构集合类来存储数据时，都是根据存储对象的hashcode值来进行判断是否相同的。所以会出现一种可能

当重写equals方法后，判断对象相等，但其hashcode却不一致，这种相等可以看作为逻辑相等。当使用hash集合类时，存放时会根据该类的hashcode方法，来确定其存放位置，如hashset，将无法过滤相同对象，因为不重写hashcode，会默认调用Object类的hashcode方法，计算出来的存放地址不一样，会导致能同时存放两个值相等的对象，产生混淆。

如果都用equals去做显然效率太低，解决方式是，每当需要对比的时候，首先hashCode去对比，如果hashCode不一样，则表示这两个对象肯定不相等（也就是不必再用equals去再对比了），如果hashCode相同，此时再对比它们的 equals，如果equals也相同，则表示这两个对象是真的相同了。

#### 接口和抽象类的区别

1. 接口的方法默认是 public，所有方法在接口中不能有实现(Java 8 开始接口方法可以有默认实现），而抽象类可以有非抽象的方法。
2. 接口中除了 static、final 变量，不能有其他变量，而抽象类中则不一定。
3. 一个类可以实现多个接口，但只能实现一个抽象类。接口自己本身可以通过 extends 关键字扩展多个接口。
4. 接口方法默认修饰符是 public，抽象方法可以有 public、protected 和 default 这些修饰符（抽象方法就是为了被重写所以不能使用 private 关键字修饰！）。
5. 从设计层面来说，**抽象是对类的抽象，是一种模板设计(自上而下)，而接口是对行为的抽象，是一种行为的规范。(自下而上)**

#### 异常

![img](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/2020-12/Java%E5%BC%82%E5%B8%B8%E7%B1%BB%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84%E5%9B%BE.png)

##### Error（错误）

**是程序无法处理的错误** 

#####  **Exception（异常）** 

 **是程序本身可以处理的异常** 

#### 吞吐量、TPS、QPS、并发数、响应时间、吞吐率

一、**QPS**: 每秒钟处理完请求的次数；注意这里是处理完。具体是指发出请求到服务器处理完成功返回结果。可以理解在server中有个counter，每处理一个请求加1，1秒后counter=QPS。

二、**TPS**：每秒钟处理完的事务次数，一般TPS是对整个系统来讲的。一个应用系统1s能完成多少事务处理，一个事务在分布式处理中，可能会对应多个请求，对于衡量单个接口服务的处理能力，用QPS比较多。

三、 **并发数**：系统能同时处理的请求数

四、RT：**响应时间**，处理一次请求所需要的平均处理时间

五、**吞吐率**
我们一般使用单位时间内服务器处理的请求数来描述其并发处理能力（**每秒处理请求数**）。称之为吞吐率（Throughput），单位是 “req/s”。吞吐率特指Web服务器单位时间内处理的请求数。
另一种描述，吞吐率是，单位时间内网络上传输的数据量，也可以指单位时间内处理客户请求数量。它是衡量网络性能的重要指标。通常情况下，吞吐率“字节数/秒”来衡量。当然你也可以用“请求数/秒”和“页面数/秒”来衡量。其实不管一个请求还是一个页面，它的本质都是在网络上传输的数据，那么用来表述数据的单位就是字节数。

六、**吞吐量**
吞吐量，是指在一次性能测试过程中网络上传输的数据量的总和

例子：
**QPS（TPS）= 并发数/平均响应时间 或者 并发数 = QPS*平均响应时间**

### 设计模式

#### 单例模式

**双重校验锁实现对象单例（线程安全）**

```java
public class Singleton {

    private volatile static Singleton uniqueInstance;

    private Singleton() {
    }

    public  static Singleton getUniqueInstance() {
       //先判断对象是否已经实例过，没有实例化过才进入加锁代码
        if (uniqueInstance == null) {
            //类对象加锁
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

另外，需要注意 `uniqueInstance` 采用 `volatile` 关键字修饰也是很有必要。还用到了**双重校验锁**。

使用 `volatile` 可以禁止 JVM 的指令重排，保证在多线程环境下也能正常运行。

**使用单例模式的好处:**

- 对于频繁使用的对象，可以**省略创建对象所花费的时间**，这对于那些重量级对象而言，是非常可观的一笔系统开销；
- 由于 new 操作的次数减少，因而对系统内存的使用频率也会降低，这将**减轻 GC 压力**，缩短 GC 停顿时间。

#### 工厂模式

**普通工厂模式**，就是建立一个工厂类，对实现了同一接口的一些类进行实例的创建

**多个工厂方法模式**，是对普通工厂方法模式的改进，在普通工厂方法模式中，如果传递的字符串出错，则不能正确创建对象，而多个工厂方法模式是提供多个工厂方法

***静态工厂方法模式***，将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可

#### 代理模式

为某对象提供一种代理以控制对该对象的访问，利用**反射**原理，买房子找中介一个道理

#### 观察者模式

指多个对象间存在一对多的依赖关系，**当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新**。这种模式有时又称作发布-订阅模式、模型-视图模式，它是对象行为型模式

#### 装饰模式

就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口。装饰对象持有被装饰对象的实例

#### 模板模式

**定义一个操作中的算法骨架**，而将算法的一些步骤延迟到子类中，使得子类可以不改变该算法结构的情况下重定义该算法的某些特定步骤

一个抽象类中，有一个主方法，再定义1...n个方法，可以是抽象的，也可以是实际的方法，定义一个类，继承该抽象类，重写抽象方法，通过调用抽象类，实现对子类的调用

#### 建造者模式

**将一个复杂对象的构造与它的表示分离，使同样的构建过程可以创建不同的表示**，这样的设计模式被称为建造者模式。它是将一个复杂的对象分解为多个简单的对象，然后一步一步构建而成

#### 策略模式

策略模式是一种行为型模式，它将对象和行为分开，将行为定义为 `一个行为接口` 和 `具体行为的实现`。策略模式最大的特点是行为的变化，行为之间可以相互替换。每个if判断都可以理解为就是一个策略。

实现：定义一个父接口，多个不同的子类实现，再定义一个策略类，私有父接口属性，有构造方法，调构造方法根据传入子类类名不同返回不同实现类。

### I/O流

#### 	BIO

同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成

#### 	NIO

NIO是一种同步非阻塞的I/O模型，支持面向**缓冲**，基于**通道的 I/O** 操作方法 

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0f483f2437ce4ecdb180134270a00144~tplv-k3u1fbpfcp-watermark.image)

#### 	AIO

AIO是异步非阻塞的IO模型，异步 IO 是基于事件和回调机制实现的，selector监听所有事件。

#### 多路I/O复用 select/poll/epoll 区别

多路复用技术：**同一个线程内同时处理多个IO请求的目的**

(1)select==>时间复杂度O(n)

它仅仅知道了，有I/O事件发生了，却并不知道是哪那几个流（可能有一个，多个，甚至全部），我们只能无差别轮询所有流，找出能读出数据，或者写入数据的流，对他们进行操作。所以**select具有O(n)的无差别轮询复杂度**，同时处理的流越多，无差别轮询时间就越长。

(2)poll==>时间复杂度O(n)

poll本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态， **但是它没有最大连接数的限制**，原因是它是基于链表来存储的

(3)epoll==>时间复杂度O(1)

**epoll可以理解为event poll**，不同于忙轮询和无差别轮询，epoll会把哪个流发生了怎样的I/O事件**通知**我们。所以我们说epoll实际上是**事件驱动（每个事件关联上fd）**的，此时我们对这些流的操作都是有意义的。**（复杂度降低到了O(1)）**

#### Netty 

1. Netty 是一个 **基于 NIO** 的 client-server(客户端服务器)框架，使用它可以快速简单地开发网络应用程序。
2. 它极大地简化并优化了 TCP 和 UDP 套接字服务器等网络编程,并且性能以及安全性等很多方面甚至都要更好。
3. **支持多种协议** 如 FTP，SMTP，HTTP 以及各种二进制和基于文本的传统协议。

##### 优点

- 统一的 API，支持多种传输类型，阻塞和非阻塞的。
- 简单而强大的线程模型。
- 自带编解码器解决 TCP 粘包/拆包问题。
- 自带各种协议栈。
- 真正的无连接数据包套接字支持。
- 比直接使用 Java 核心 API 有更高的吞吐量、更低的延迟、更低的资源消耗和更少的内存复制。
- 安全性不错，有完整的 SSL/TLS 以及 StartTLS 支持。
- 社区活跃
- 成熟稳定，经历了大型项目的使用和考验，而且很多开源项目都使用到了 Netty， 比如我们经常接触的 Dubbo、RocketMQ 等等。

##### Netty 应用场景

 NIO 可以做的事情 ，使用 Netty 都可以做并且更好。Netty 主要用来做**网络通信** : 

1. **作为 RPC 框架的网络通信工具** ： 我们在分布式系统中，不同服务节点之间经常需要相互调用，这个时候就需要 RPC 框架了。不同服务指点的通信是如何做的呢？可以使用 Netty 来做。比如我调用另外一个节点的方法的话，至少是要让对方知道我调用的是哪个类中的哪个方法以及相关参数吧！
2. **实现一个自己的 HTTP 服务器** ：通过 Netty 我们可以自己实现一个简单的 HTTP 服务器，这个大家应该不陌生。说到 HTTP 服务器的话，作为 Java 后端开发，我们一般使用 Tomcat 比较多。一个最基本的 HTTP 服务器可要以处理常见的 HTTP Method 的请求，比如 POST 请求、GET 请求等等。
3. **实现一个即时通讯系统** ： 使用 Netty 我们可以实现一个可以聊天类似微信的即时通讯系统，这方面的开源项目还蛮多的，可以自行去 Github 找一找。
4. **实现消息推送系统** ：市面上有很多消息推送系统都是基于 Netty 来做的。

### 数据结构

#### String、Stringbuffer、StringBuild区别

1. 操作少量的数据: 适用 `String`

2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`

3. **多线程**操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`

   ![img](https://img-blog.csdnimg.cn/img_convert/929c61df35d191d7d7cbd9e6d51306c1.png)

#### List

 存储的元素是有序的、可重复的 

##### Arraylist

非线性安全，底层使用 `Object[]`数组实现，长度增长一半

**初始化**

ArrayList的底层是一个**动态数组**，ArrayList首先会对传进来的初始化参数initalCapacity进行判断

如果参数等于0，则将数组初始化为一个**空数组**，
如果不等于0，将数组初始化为一个**容量为10的数组**。

**扩容时机**

当数组的大小大于初始容量的时候(比如初始为10，当添加第11个元素的时候)，就会进行扩容，新的容量为旧的容量的**1.5倍**。

**扩容方式**

 扩容的时候，会以新的容量建一个原数组的**拷贝**，修改原数组，指向这个新数组，原数组被抛弃，会被GC回收。

##### LinkedList

非线性安全， **双向链表**(JDK1.6 之前为循环链表，JDK1.7 取消了循环) ，**ConcurrentLinkedQueue 线性安全**

##### Vector

线性安全，`Object[]`数组，长度增长一倍， **CopyOnWriteArrayList** 性能更好

#### Map

 使用键值对（kye-value）存储 

##### HashMap

线程不安全，允许一个null键，多个null值，初始化大小为16。之后每次扩充，容量变为原来的2倍，结构为**数组加链表**（链表散列），**链表长度大于阈值（默认为8）时 且 数据总量大于64时**，将链表转化为红黑树，以减少搜索时间

**扩容**：当hashmap中的元素个数超过数组大小*loadFactor时，就会进行数组扩容，**loadFactor的默认值为0.75**，也就是说，默认情况下，数组大小为16，那么当hashmap中元素个数超过16✖️0.75=12的时候，就把数组的大小扩展为2✖️16=32，即扩大一倍

比如说我们有1000个元素new HashMap(1000), 但是理论上来讲new HashMap(1024)更合适，即使是1000，hashmap也自动会将其设置为1024。 但是new HashMap(1024)还不是更合适的，因为0.75✖️1000 < 1000, 也就是说为了让0.75 * size > 1000, 我们必须这样new HashMap(2048)才最合适，既考虑了性能的问题，也避免了resize的问题。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200502112926682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1ZpbmNlX1dhbmcx,size_16,color_FFFFFF,t_70)

###### HashMap为什么线程不安全？

1、多线程下扩容死循环。JDK1.7中的HashMap使用头插法插入元素，在多线程的环境下，扩容的时候有可能导致环形链表的出现，形成死循环。因此JDK1.8使用尾插法插入元素，在扩容时会保持链表元素原本的顺序，不会出现环形链表的问题

2、多线程的put可能导致元素的丢失。多线程同时执行put操作，如果计算出来的索引位置是相同的，那会造成前一个key被后一个key覆盖，从而导致元素的丢失。此问题在JDK1.7和JDK1.8中都存在

3、put和get并发时，可能导致get为null。线程1执行put时，因为元素个数超出threshold而导致rehash，线程2此时执行get，有可能导致这个问题，此问题在JDK1.7和JDK1.8中都存在

注：一般用**Integer、String这种不可变类**当HashMap当key

###### **解决hash冲突**

当拿到一个hash值，通过indexFor(hash, table.length)获取数组下标，先查询是否存在该hash值，若不存在，则直接以Entry<V,V>的方式存放在数组中，若存在，则再对比key是否相同,若hash值和key都相同，则替换value，若hash值相同，key不相同，则形成一个单链表，将hash值相同，key不同的元素以Entry<V,V>的方式存放在链表中，这样就解决了hash冲突，这种方法叫做**分离链表法**

![ ](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/put%E6%96%B9%E6%B3%95.png)

##### ConcurrentHashMap 

**线性安全的HashMap**

 在 JDK1.7 的时候，ConcurrentHashMap（**分段锁**） 对整个桶数组进行了分割分段(Segment)，每一把锁只锁容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。到了 JDK1.8 的时候已经摒弃了 Segment 的概念，而是直接用 Node 数组+链表+红黑树的数据结构来实现，并发控制使用 **synchronized 和 CAS **来操作。（JDK1.6 以后 对 synchronized 锁做了很多优化） 整个看起来就像是优化过且线程安全的 HashMap 

**注**：当链表长度大于阈值（默认为 8）并且 HashMap 数组长度超过 64 的时候才会执行链表转红黑树的操作，否则就只是对数组扩容。

#####  LinkedHashMap 

 继承自 `HashMap` ，在 `HashMap` 基础上增加了一条双向链表 ，HashMap无序；LinkedHashMap有序。

##### HashTable

数组+链表组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的 

**线程安全**，内部的方法基本都经过synchronized 修饰，不允许null键，null值，初始大小为11，之后每次扩充，容量变为原来的2n+1 

##### TreeMap 

 红黑树 

#### Set

 存储的元素是无序的、不可重复的 

`HashSet`（无序，唯一）: 基于 `HashMap` 实现的，底层采用 `HashMap` 来保存元素

`LinkedHashSet`：`LinkedHashSet` 是 `HashSet` 的子类，并且其内部是通过 `LinkedHashMap` 来实现的。有点类似于我们之前说的 `LinkedHashMap` 其内部是基于 `HashMap` 实现一样，不过还是有一点点区别的

`TreeSet`（有序，唯一）： 红黑树(自平衡的排序二叉树)

#### 快速失败&安全失败

##### 快速失败

 快速失败(fail-fast) 是 Java 集合的一种错误检测机制。在使用迭代器对集合进行遍历的时候，我们在多线程下操作非安全失败(fail-safe)的集合类可能就会触发 fail-fast 机制，导致抛出 `ConcurrentModificationException` 异常。 另外，在单线程下，如果在遍历过程中对集合对象的内容进行了修改的话也会触发 fail-fast 机制。

##### 安全失败

 采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。所以，在遍历过程中对原集合所作的修改并不能被迭代器检测到，故不会抛 `ConcurrentModificationException` 异常。 

#### 深拷贝和浅拷贝

**浅拷贝**（shallowCopy）只是增加了一个指针指向已存在的内存地址，

**深拷贝**（deepCopy）是增加了一个指针并且申请了一个新的内存，使这个增加的指针指向这个新的内存

### Spring

**Spring 是一款开源的轻量级 Java 开发框架，旨在提高开发人员的开发效率以及系统的可维护性。**

一些重要的Spring Framework模块是：核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块 

- **Spring Core：** 基础,可以说 Spring 其他所有的功能都需要依赖于该类库。主要提供 IOC 依赖注入功能。
- **Spring Aspects** ： 该模块为与AspectJ的集成提供支持。
- **Spring AOP** ：提供了面向方面的编程实现。
- **Spring JDBC** : Java数据库连接。
- **Spring JMS** ：Java消息服务。
- **Spring ORM** : 用于支持Hibernate等ORM工具。
- **Spring Web** : 为创建Web应用程序提供支持。
- **Spring Test** : 提供了对 JUnit 和 TestNG 测试的支持。

#### IoC 和 AOP

 **IoC**（Inverse of Control:控制反转）或者称为：**依赖注入**，是一种**设计思想**，就是 **将原本在程序中手动创建对象的控制权，交由Spring框架来管理**。 IoC 容器实际上就是个Map（key，value）,在Map 中存放的是各种对象。 IOC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。

 **AOP**(Aspect-Oriented Programming:面向切面编程)**能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来**，便于**减少系统的重复代码**，**降低模块间的耦合度**，并**有利于未来的可拓展性和可维护性**。 

#### **依赖注入方式**：

- 构造器注入 --@Autowired加在controller的构造上，调用service的构造
- Setter方法注入 --@Autowired加在service的setter方法上
- 属性注入--使用@Autowired实现，只能用在Ioc容器上

#### **BeanFactory和FactoryBean区别**

BeanFactory是个Factory，也就是IOC容器或对象工厂，FactoryBean是个Bean。在Spring中，所有的Bean都是由BeanFactory(也就是IOC容器)来进行管理的。但对FactoryBean而言，这个Bean不是简单的Bean，而是一个能生产或者修饰对象生成的工厂Bean,它的实现与设计模式中的工厂模式和修饰器模式类似。

#### JDK 动态代理和 CGLIB 动态代理对比

1. **JDK 动态代理只能代理实现了接口的类或者直接代理接口，而 CGLIB 可以代理未实现任何接口的类。** 另外， CGLIB 动态代理是通过生成一个被代理类的子类来拦截被代理类的方法调用，因此不能代理声明为 final 类型的类和方法。
2. 就二者的效率来说，大部分情况都是 **JDK 动态代理更优秀**，随着 JDK 版本的升级，这个优势更加明显。

**在 CGLIB 动态代理机制中 `MethodInterceptor` 接口和 `Enhancer` 类是核心**

**在 Java 动态代理机制中 `InvocationHandler` 接口和 `Proxy` 类是核心。**

CGLIB底层使用了**ASM**（一个短小精悍的字节码操作框架）来**操作字节码**生成新的类

JDK动态代理，只能对接口进行代理。如果要代理的类为一个普通类、没有接口，那么Java动态代理就没法使用了

Spring AOP 功能的实现就是动态代理

#### 事务管理

1、编程式事务管理

2、声明式事务管理（推荐），@Transactional、xml

**BeanFactory、ApplicationContext两者装载 bean 的区别：** 

* BeanFactory ：在启动时不会去实例化 Bean ，只有从容器中获取 Bean 时才会去实例化。 
* ApplicationContext ：在启动的时候就把所有的 Bean 全部实例化了 。 它还可以为 Bean 配置 lazy-init=true 来让 Bean 延迟实例化。

#### 事务失效情况

- spring的事务注解@Transactional只能放在**public**修饰的方法上才起作用，如果放在其他非public（private，protected）方法上，虽然不报错，但是事务不起作用
- **数据库存储引擎需要支持事务**，如使用mysql且引擎是MyISAM，则事务会不起作用，原因是MyISAM不支持事务，可以改成InnoDB引擎
- 没有被 Spring 管理，没有加@Service注解
- 方法中异常被捕捉，或者抛出的异常不是默认的RunTimeException，可以自己在注解上加配置
- 没有运行事务，以NOT_SUPPORTED运行
- 发生了自身调用，没有被spring管理，默认只有在外部调用事务才会生效

#### Spring 事务的传播属性

所谓spring事务的传播属性，就是定义在存在多个事务同时存在的时候，spring应该如何处理这些事务的行为。这些属性在TransactionDefinition中定义，具体常量的解释见下表：

| 行为          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| REQUIRED      | 如果有事务在运行，当前的方法就在这个事务内运行，否则，就启动一个新的事务，并在自己的事务内运行 |
| SUPPORTS      | 如果有事务在运行，当前的方法就在这个事务内运行；如果当前没有事务，则以非事务的方式运行。 |
| MANDATORY     | 如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。 |
| REQUIRES_NEW  | 当前的方法必须启动新事务，并在它自己的事务内运行，如果有事务正在运行，应该将它挂起 |
| NOT_SUPPORTED | 以非事务方式运行，如果当前存在事务，则把当前事务挂起。       |
| NEVER         | 以非事务方式运行，如果当前存在事务，则抛出异常。             |
| NESTED        | 如果当前存在事务，则创建一个新事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于 REQUIRED。 |

根据上面的描述，我们可以将行为分为三大类。

- 不要事务：NEVER、NOT_SUPPORTED。
- 如果有则用：SUPPORTS
- 必须使用事务：REQUIRED、REQUIRES_NEW、NESTED、MANDATORY

#### bean作用域

- **singleton** : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
- **prototype** :（原型对象） 每次请求都会创建一个新的 bean 实例。
- **request** : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效。
- **session** : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。
- **global-session**： 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话

#### BEAN生命周期

1. **Spring启动，查找并加载需要被Spring管理的bean，进行Bean的实例化**
2. Bean实例化后对**将Bean的引入和值注入到Bean的属性中**
3. 如果Bean实现了BeanNameAware接口的话，Spring将Bean的Id传递给setBeanName()方法
4. 如果Bean实现了BeanFactoryAware接口的话，Spring将调用setBeanFactory()方法，将BeanFactory容器实例传入
5. 如果Bean实现了ApplicationContextAware接口的话，Spring将调用Bean的setApplicationContext()方法，将bean所在应用上下文引用传入进来。
6. 如果Bean实现了BeanPostProcessor接口，Spring就将调用他们的postProcessBeforeInitialization()方法。
7. 如果Bean 实现了InitializingBean接口，Spring将调用他们的afterPropertiesSet()方法。类似的，如果bean使用init-method声明了初始化方法，该方法也会被调用
8. 如果Bean 实现了BeanPostProcessor接口，Spring就将调用他们的postProcessAfterInitialization()方法。
9. 此时，**Bean已经准备就绪，可以被应用程序使用了。他们将一直驻留在应用上下文中，直到应用上下文被销毁**。
10. 如果bean实现了DisposableBean接口，Spring将调用它的destory()接口方法，同样，如果**bean使用了destory-method 声明销毁方法**，该方法也会被调用。

![Spring Bean 生命周期](https://images.xiaozhuanlan.com/photo/2019/b5d264565657a5395c2781081a7483e1.jpg)

#### Spring用到了哪些设计模式

- **工厂设计模式** : Spring使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。

- **代理设计模式** : 

  **Spring AOP 就是基于动态代理的**，如果要代理的对象，实现了某个接口，那么Spring AOP会使用**JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候Spring AOP会使用 **Cglib** 生成一个被代理对象的子类来作为代理

- **单例设计模式** : Spring 中的 Bean 默认都是单例的。

- **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。（JDBC使用桥接模式）

- **包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。

- **观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。

- **适配器模式** :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。

#### Spring中单例Bean的三级缓存

- 第一级缓存〈也叫单例池）singletonObjects:存放已经经历了完整生命周期的Bean对象
- 第二级缓存: earlySingletonObjects，存放早期暴露出来的Bean对象，Bean的生命周期未结束（属性还未填充完整）
- 第三级缓存: Map<String, ObiectFactory<?>> singletonFactories，存放可以生成Bean的工厂

#### Spring如何解决循环依赖

1. A创建过程中需要B，于是**A将自己放到三级缓存**里面，去**实例化B**
2. B实例化的时候发现需要A，于是B先查一级缓存，没有，再查二级缓存，还是没有，再查三级缓存，找到了A然后把三级缓存里面的这个**A放到二级缓存里面，并删除三级缓存里面的A**
3. **B顺利初始化完毕**，将自己放到一级缓存里面（**此时B里面的A依然是创建中状态**）然后回来接着创建A，此时B已经创建结束，直接从一级缓存里面拿到B，然后完成创建，并**将A放到一级缓存**中。

### SpringMVC

Spring MVC主要由DispatcherServlet、处理器映射、处理器(控制器)、视图解析器、视图组成。他的两个核心是两个核心：

处理器映射：选择使用哪个控制器来处理请求
视图解析器：选择结果应该如何渲染

通过以上两点，Spring MVC保证了如何选择控制处理请求和如何选择视图展现输出之间的松耦合。

![这里写图片描述](https://img-blog.csdn.net/20160427094830780)

(1) Http请求：客户端请求提交到DispatcherServlet。
(2) 寻找处理器：由DispatcherServlet控制器查询一个或多个HandlerMapping，找到处理请求的Controller。
(3) 调用处理器：DispatcherServlet将请求提交到Controller。
(4)(5)调用业务处理和返回结果：Controller调用业务逻辑处理后，返回ModelAndView。
(6)(7)处理视图映射并返回模型： DispatcherServlet查询一个或多个ViewResoler视图解析器，找到ModelAndView指定的视图。
(8) Http响应：视图负责将结果显示到客户端。

### 自定义注解

#### 一、创建注解

需要@interface声明，启动类上增加`@EnableAspectJAutoProxy(exposeProxy=true,proxyTargetClass=true)`

`@Retention`: 表示该注解的生命周期，SOURCE < CLASS < RUNTIME，我们一般用RUNTIME

`@Target`: 表示该注解的作用范围

- `ElementType.FIELD`:用于接口、类、枚举、注解
- `ElementType.TYPE`:用于字段、枚举的常量
- `ElementType.PARAMETER`:用于方法参数
- `ElementType.METHOD`:用于方法

#### 二、定义注解行为

如何去处理我们的注解

- @Before: 前置通知, 在方法执行之前执行，这个通知不能阻止连接点前的执行（除非它抛出一个异常）。
- @After: 后置通知, 在方法执行之后执行（不论是正常返回还是异常退出）。
- @Around: 包围一个连接点（join point）的通知，如方法调用。这是最强大的一种通知类型。 环绕通知可以在方法调用前后完成自定义的行为。它也会选择是否继续执行连接点或直接返回它们自己的返回值或抛出异常来结束执行。
- @AfterRunning:返回通知, 在方法正常返回结果之后执行 。
- @AfterThrowing: 异常通知, 在方法抛出异常之后。

## 二、分布式

 ![img](https://camo.githubusercontent.com/dab34cf13fb06452805e8a9cbb0ab7bea95691e7/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d31312f313633393233343233376563393830352e706e67) 

### 幂等性

**定义：就是用户对于同一操作发起的一次请求或者多次请求的结果是一致的，不会因为多次点击而产生了副作用**

#### 怎样保证幂等性

一、token机制

二、各种锁机制：乐观锁、悲观锁、分布式锁

三、各种唯一约束：数据库唯一约束、redis 防重、防重表、全局请求唯一ID

### 分布式事务处理

#### 两阶段提交（2PC）

准备阶段/提交阶段

 通过引入协调者（Coordinator）来协调参与者的行为，并最终决定这些参与者是否要真正执行事务。 

同步阻塞，可能出现数据不一致

#### 三阶段提交（3PC）

询问阶段/准备阶段/提交阶段

先询问事务参与者能否执行数据库操作，再执行，最后协调组决定是否提交

引入超时机制避免阻塞

#### 补偿事务（TCC）（框架ByteTCC）

针对每个操作，都要注册一个与其对应的确认和补偿（撤销）操作。它分为三个阶段：

- Try 阶段主要是对业务系统做检测及资源预留
- Confirm 阶段主要是对业务系统做确认提交，Try阶段执行成功并开始执行 Confirm阶段时，默认 Confirm阶段是不会出错的。即：只要Try成功，Confirm一定成功。
- Cancel 阶段主要是在业务执行错误，需要回滚的状态下执行的业务取消，预留资源释放。

#### 本地消息表（异步确保）

 本地消息表与业务数据表处于同一个数据库中，这样就能利用本地事务来保证在对这两个表的操作满足事务特性，并且使用了消息队列来保证最终一致性。 

#### MQ 事务消息

 RocketMQ，支持事务消息的方式也是类似于采用的二阶段提交，比如 RabbitMQ 和 Kafka 都不支持。 

### 分布式ID生成

1. 最基本的分布式 ID 需要满足下面这些要求：
   - **全局唯一** ：ID 的全局唯一性肯定是首先要满足的！
   - **高性能** ： 分布式 ID 的生成速度要快，对本地资源消耗要小。
   - **高可用** ：生成分布式 ID 的服务要保证可用性无限接近于 100%。
   - **方便易用** ：拿来即用，使用方便，快速接入！
2. 常见解决方案
   - 数据库主键自增，通过关系型数据库的自增主键产生来唯一的 ID
   - **Redis 方案**
   - java自带UUID
   - 雪花算法
     - UidGenerator 是百度开源的一款基于 Snowflake(雪花算法)的唯一 ID 生成器。
     - Leaf 提供了 **号段模式** 和 **Snowflake(雪花算法)** 这两种模式来生成分布式 ID

### 微服务

##### **SPI** 

具体原理是这样的：**我们将接口的实现类放在配置文件中，在程序运行过程中读取配置文件，通过反射加载实现类**。这样，我们可以在运行的时候，动态替换接口的实现类。和 IoC 的解耦思想是类似的。

#### 1、Dubbo

是一款高性能、轻量级的开源Java RPC 框架，它提供了三大核心能力：**面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现**。简单来说 Dubbo 是一个分布式服务框架，致力于提供高性能和透明化的RPC远程服务调用方案，以及SOA服务治理方案。 

![dubbo-relation](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/%E6%BA%90%E7%A0%81/dubbo/dubbo-relation.jpg)

上述节点简单介绍以及他们之间的关系：

- **Container：** 服务运行容器，负责加载、运行服务提供者。必须。
- **Provider：** 暴露服务的服务提供方，会向注册中心注册自己提供的服务。必须。
- **Consumer：** 调用远程服务的服务消费方，会向注册中心订阅自己所需的服务。必须。
- **Registry：** 服务注册与发现的注册中心。注册中心会返回服务提供者地址列表给消费者。非必须。
- **Monitor：** 统计服务的调用次数和调用时间的监控中心。服务消费者和提供者会定时发送统计数据到监控中心。 非必须。

**Invoker** 是 Dubbo 领域模型中非常重要的一个概念，`Invoker` 就是 Dubbo 对远程调用的抽象

**寻址、单一长连接、传输协议：TCP、传输方式：NIO（Netty），协议默认使用Dubbo，序列化默认hessian2**

##### 特性

1. **负载均衡**——同一个服务部署在不同的机器时该调用那一台机器上的服务。
2. **服务调用链路生成**——随着系统的发展，服务越来越多，服务间依赖关系变得错踪复杂，甚至分不清哪个应用要在哪个应用之前启动，架构师都不能完整的描述应用的架构关系。Dubbo 可以为我们解决服务之间互相是如何调用的。
3. **服务访问压力以及时长统计、资源调度和治理**——基于访问压力实时管理集群容量，提高集群利用率。
4. **服务降级**——某个服务挂掉之后调用备用服务。

#####  ZooKeeper 作为注册中心

简介：是一种用于分布式应用程序的高性能协调服务，提供一种集中式信息存储服务

特点：数据存储在内存中，类似文件系统的树形结构，高吞吐量和低延迟，集群高可靠

作用：基于zookeeper可以实现分布式统一配置中心、服务注册中心、分布式锁等功能。

注：

2. ZooKeeper 是 Hadoop 生态系统的一员；
3. 构建 ZooKeeper 集群的时候，是主从结构，使用的服务器最好是奇数台。

###### 特点

- **顺序一致性：** 从同一客户端发起的事务请求，最终将会严格地按照顺序被应用到 ZooKeeper 中去。
- **原子性：** 所有事务请求的处理结果在整个集群中所有机器上的应用情况是一致的，也就是说，要么整个集群中所有的机器都成功应用了某一个事务，要么都没有应用。
- **单一系统映像 ：** 无论客户端连到哪一个 ZooKeeper 服务器上，其看到的服务端数据模型都是一致的。
- **可靠性：** 一旦一次更改请求被应用，更改的结果就会被持久化，直到被下一次更改覆盖。

###### 应用场景

1. **分布式锁** ： 通过创建唯一节点获得分布式锁，当获得锁的一方执行完相关代码或者是挂掉之后就释放锁。
2. **命名服务** ：可以通过 ZooKeeper 的顺序节点生成全局唯一 ID
3. **数据发布/订阅** ：通过 **Watcher 机制** 可以很方便地实现数据发布/订阅。当你将数据发布到 ZooKeeper 被监听的节点上，其他机器可通过监听 ZooKeeper 上节点的变化来实现配置的动态更新。

应用案例：

1. Hbase(分布式的、面向列的开源数据库)：进行master选举、服务间协调
2. Solr(全文搜索服务器-大数据)：进行集群管理、Leader选举、配置管理
3. Dubbo(微服务)：服务注册
4. Mycat(分布式数据库系统、分库分表)：集群管理、配置管理
5. Sharding-sphere(分布式数据库中间件、分库分表)：集群管理、配置管理

###### 选举机制

根据权重来选举老大，超过半数加一就可以成为领导，后面的权重再大也要服从

- ServiceID服务器ID
- Zxid数据ID，编号越大权重越大
- Epoch逻辑时钟，投票次数
- Server状态(LOOKING竞选状态、FOLLOWING随从状态、OBSERVING观察状态、LEADING领导者状态)

#### 2、SpringBoot

Spring Boot 基本上是 Spring 框架的扩展，它消除了设置 Spring 应用程序所需的 XML配置，为更快，更高效的开发生态系统铺平了道路。 以下是 Spring Boot 中的一些特点：

1. 创建独立的 spring 应用。 
2. 嵌入 Tomcat , Jetty Undertow 而且不需要部署他们. 
3. 提供的“starters” poms来简化 Maven 配置 
4. 尽可能自动配置 spring 应用。 
5. 提供生产指标,健壮检查和外部化配置 
6. 绝对没有代码生成和 XML 配置要求

##### Spring Boot的主要优点

1. 开发基于 Spring 的应用程序很容易。
2. Spring Boot 项目所需的开发或工程时间明显减少，通常会提高整体生产力。
3. Spring Boot不需要编写大量样板代码、XML配置和注释。
4. Spring引导应用程序可以很容易地与Spring生态系统集成，如Spring JDBC、Spring ORM、Spring Data、Spring Security等。
5. Spring Boot遵循“固执己见的默认配置”，以减少开发工作（默认配置可以修改）。
6. Spring Boot 应用程序提供嵌入式HTTP服务器，如Tomcat和Jetty，可以轻松地开发和测试web应用程序。（这点很赞！普通运行Java程序的方式就能运行基于Spring Boot web 项目，省事很多）
7. Spring Boot提供命令行接口(CLI)工具，用于开发和测试Spring Boot应用程序，如Java或Groovy。
8. Spring Boot提供了多种插件，可以使用内置工具(如Maven和Gradle)开发和测试Spring Boot应用程序。

##### springboot启动流程

第一部分进行SpringApplication的**初始化**模块，配置一些基本的环境变量、资源、构造器、监听器，

第二部分实现了应用具体的启动方案，包括启动流程的监听模块、加载配置环境模块、及核心的创建上下文环境模块，

第三部分是**自动化配置模块**，该模块作为SpringBoot自动配置核心，在后面的分析中会详细讨论。在下面的启动程序中我们会串联起结构中的主要功能。

具体如下：

每个SpringBoot程序都有一个主入口，也就是main方法，main里面调用SpringApplication.run()启动整个spring-boot程序，该方法所在类需要使用@SpringBootApplication注解，以及@ImportResource注解(if need)，

@SpringBootApplication包括三个注解，功能如下：

- @EnableAutoConfiguration：SpringBoot根据应用所声明的依赖来对Spring框架进行自动配置
- @SpringBootConfiguration(内部为@Configuration)：被标注的类等于在spring的XML配置文件中(applicationContext.xml)，装配所有bean事务，提供了一个spring的上下文环境
- @ComponentScan：组件扫描，可自动发现和装配Bean，默认扫描SpringApplication的run方法里的Booter.class所在的包路径下文件，所以最好将该启动类放到根包路径下

##### 常用注解

**SpringBootApplication**

**MapperScan**

**Controller、RequestMapping、ResponseBody**

**Autowired、Component、Repository**

**Service**

**Transactional**

**@Autowired的原理：**其实在启动spring IoC时，容器自动装载了一个AutowiredAnnotationBeanPostProcessor后置处理器，当容器扫描到@Autowied、@Resource(是CommonAnnotationBeanPostProcessor后置处理器处理的)或@Inject时，就会在IoC容器自动查找需要的bean，并装配给该对象的属性

**@Autowired 与@Resource的区别**： 

1、 @Autowired与@Resource都可以用来装配bean. 都可以写在字段上,或写在setter方法上。

2、 @Autowired**默认按类型(byType)装配**（这个注解是属业spring的），默认情况下必须要求依赖对象必须存在，如果要允许null值，可以设置它的required属性为false，如：@Autowired(required=false) ，如果我们想使用名称装配可以结合@Qualifier注解进行使用，如下：

```java
@Autowired ()
@Qualifier ( "baseDao" )
private BaseDao baseDao;
```

3、@Resource（这个注解属于J2EE的），**默认按照名称(byName)进行装配**，名称可以通过name属性进行指定，如果没有指定name属性，当注解写在字段上时，默认取字段名进行安装名称查找，如果注解写在setter方法上默认取属性名进行装配。当找不到与名称匹配的bean时才按照类型进行装配。但是需要注意的是，如果name属性一旦指定，就只会按照名称进行装配。Java11就废弃了，统一使用@Autowired

```java
@Resource(name="baseDao")
private BaseDao baseDao;
```

##### 自动装配

Spring Boot 通过`@EnableAutoConfiguration`开启自动装配，通过 SpringFactoriesLoader 最终加载`META-INF/spring.factories`中的自动配置类实现自动装配，自动配置类其实就是通过`@Conditional`按需加载的配置类，想要其生效必须引入`spring-boot-starter-xxx`包实现起步依赖

![在这里插入图片描述](https://img-blog.csdnimg.cn/4c7373f48f534758a5a9c52f42bb3a08.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5aSn56We5oiR5Lmf,size_20,color_FFFFFF,t_70,g_se,x_16)

##### SpringBoot与SpringCloud区别	

1. Spring boot是Spring的一套**快速配置脚手架**，可以基于Spring Boot快速开发单个微服务；Spring Cloud是一个基于Spring Boot实现的云应用开发工具
2. Spring Boot专注于**快速、方便**集成的单个个体,Spring Cloud是关注全局的服务治理框架；
3. Spring boot使用了**默认大于配置**的理念，很多集成方案已经帮你选择好了，能不配置就不配置，Spring Cloud很大的一部分是基于Spring Boot来实现。
4. Spring Boot可以离开Spring Cloud独立使用开发项目，但是Spring Cloud离不开Spring Boot,属于依赖的关系。

#### 3、Spring cloud

优点：

1、服务拆分粒度更细，有利于资源重复利用，有利于提高开发效率

2、可以更精准的制定优化服务方案，提高系统的可维护性

3、微服务架构采用去中心化思想，服务之间采用Restful等轻量级通讯，比ESB更轻量

4、适于互联网时代，产品迭代周期更短

缺点：

1、微服务过多，治理成本高，不利于维护系统

2、分布式系统开发的成本高（容错，分布式事务等）对团队挑战大

 服务系统架构的一站式解决方案，在平时我们构建微服务的过程中需要做如 **服务发现注册** 、**配置中心** 、**消息总线** 、**负载均衡** 、**断路器** 、**数据监控** 等操作，而 Spring Cloud 为我们提供了一套简易的编程模型，使我们能在 Spring Boot 的基础上轻松地实现微服务项目的构建。 

##### 服务发现框架—Eureka

Eureka Server通过**Register、Get、Renew**等接口提供服务的**注册、发现和心跳检测**等服务，请求过来要走注册中心，但是消费者可以把信息缓存起来，不用每次都走注册中心。**主备或者集群实现高可用**

1. **服务注册**：eureka客户端会通过发送rest请求的方式向eureka服务端注册自身元数据：ip地址,端口,运行状况等信息,服务端会把注册信息存储在一个双层map中
2. **服务续约**：eureka客户端每30秒发送一次心跳来续约,告知客户端正常,如果eureka服务端90秒没收到心跳,则将其从注册表删除
3. **获取注册表信息**：客户端通过rest请求从服务端获取注册表信息,缓存在本地,服务调用的时候,会从注册表查找其它服务,每30秒更新一次
4. **服务调用**：客户端获取到服务清单后,就可以从中查找其它服务地址进行远程调用,会通过ribbon自动进行负载均衡
5. **eureka高可用:服务同步**：配置eureka集群,服务之间会相互注册,客户端的注册信息和续约信息被复制到集群中的所有节点,只要有一个节点活着都可以发挥注册中心的作用
6. **服务剔除**：eureka服务启动的时候创建一个定时任务,每60秒从当前服务清单中剔除续约超时的(90秒)
7. **自我保护机制**：当网络一段时间内发生了异常，所有服务都没能够续约，eureka server会把所有服务剔除，显然不太合理，所以就有了自我保护机制。服务端判断：**如果15分钟内收到的心跳请求率，如果低于85%，可能网络故障，注册表则不再删除**,但是提供正常的服务注册和查询，当恢复正常时，则取消保护机制。（注：自我保护机制会导致Eureka不再从注册列表移除因长时间没收到心跳而应该过期的服务，Eureka仍然能够接受新服务的注册和查询请求,但是不会被同步到其他节点(实现高可用性)，当网络稳定时,当前实例新的注册信息会被同步到其他节点中(最终一致性)）

Eureka Server在启动时默认会注册自己，成为一个服务，所以Eureka Server也是一个客户端。也就是说们我们可以配置多个Eureka Server，让他们之间**相互注册**，当服务提供者向其中一个Eureka注册服务时，这个服务就会被共享到其他Eureka上，这样所有的Eureka都会有相同的服务。

集群搭建：引入依赖、加上注解@EnableEurekaServer/@EnableDiscoveryClient、配置端口/名称注册URL

##### 配置中心-Config 

 将各个 应用/系统/模块 的配置文件存放到 **统一的地方然后进行管理** 

特性：

- HTTP，为外部配置提供基于资源的API(键值对，或者等价的YAML内容)
- 属性值的加密和解密(对称加密和非对称加密)
- 通过使用@EnableConfigServer在Spring boot应用中非常简单的嵌入。
- 绑定Config服务端，并使用远程的属性源初始化Spring环境。
- 属性值的加密和解密(对称加密和非对称加密)

##### 分布式配置中心 - Apollo

Apollo客户端的实现原理

![image-20210121224102611](https://img-blog.csdnimg.cn/img_convert/ae25547b3832079ba5e5d091ff288a0f.png)

1. 客户端和服务端保持了一个长连接，从而能第一时间获得配置更新的推送。(通过Http Long Polling实现)
2. 客户端还会定时从Apollo配置中心服务端拉取应用的最新配置。
   这是一个fallback机制，为了防止推送机制失效导致配置不更新
   客户端定时拉取会上报本地版本，所以一般情况下，对于定时拉取的操作，服务端都会返回304 - Not Modified
   定时频率默认为每5分钟拉取一次，客户端也可以通过在运行时指定System Property: apollo.refreshInterval来覆盖，单位为分钟
3. 客户端从Apollo配置中心服务端获取到应用的最新配置后，会保存在内存中
4. 客户端会把从服务端获取到的配置在本地文件系统缓存一份
   在遇到服务不可用，或网络不通的时候，依然能从本地恢复配置
5. 应用程序可以从Apollo客户端获取最新的配置、订阅配置更新通知

##### 负载均衡-Ribbon

Ribbon实际是封装了restTemplate，是**客户端负载均衡**，根据负载均衡算法分发请求

算法

- **`RoundRobinRule`**：轮询策略。`Ribbon` 默认采用的策略。若经过一轮轮询没有找到可用的 `provider`，其最多轮询 10 轮。若最终还没有找到，则返回 `null`。取余算下标
- **`RandomRule`**: 随机策略，从所有可用的 `provider` 中随机选择一个。
- **`RetryRule`**: 重试策略。先按照 `RoundRobinRule` 策略获取 `provider`，若获取失败，则在指定的时限内重试。默认的时限为 500 毫秒。

##### 服务间的调用-Feign

feign底层是使用了ribbon作为负载均衡的客户端，**通过http请求找到对应的服务，而不是网关**

**`Feign`—>`Hystrix` —>`Ribbon` —>`Http Client`**

##### 熔断和降级-Hystrix

通过hystrix可以解决雪崩效应问题，它提供了**资源隔离、降级机制、融断、缓存**等功能

资源隔离：包括线程池隔离和信号量隔离，限制调用分布式服务的资源使用，某一个调用的服务出现问题不会影响其他服务调用。

降级机制：超时降级、资源不足时(线程或信号量)降级，降级后可以配合降级接口返回托底数据。

融断：**当失败率达到阀值自动触发降级**(如因网络故障/超时造成的失败率高)，熔断器触发的快速失败会进行快速恢复。

缓存：返回结果缓存，后续请求可以直接走缓存。

请求合并：可以实现将一段时间内的请求（一般是对同一个接口的请求）合并，然后只对服务提供者发送一次请求。

##### 微服务网关-Zuul

Zuul提供了**动态路由、监控、弹性负载和安全功能**。Zuul底层利用各种filter实现如下功能：

- 认证和安全 识别每个需要认证的资源，拒绝不符合要求的请求。
- 性能监测 在服务边界追踪并统计数据，提供精确的生产视图。
- 动态路由 根据需要将请求动态路由到后端集群。
- 压力测试 逐渐增加对集群的流量以了解其性能。
- 负载卸载 预先为每种类型的请求分配容量，当请求超过容量时自动丢弃。
- 静态资源处理 直接在边界返回某些响应。

 **路由和过滤器**

使用的是阻塞式的 API，不支持长连接，比如 websockets。

底层是servlet，Zuul处理的是http请求

没有提供异步支持，流控等均由hystrix支持。

依赖包spring-cloud-starter-netflix-zuul。

##### Gateway：

Spring Boot和Spring Webflux提供的Netty底层环境，不能和传统的Servlet容器一起使用，也不能打包成一个WAR包。

依赖spring-boot-starter-webflux和/ spring-cloud-starter-gateway

提供了异步支持，提供了抽象负载均衡，提供了抽象流控，并默认实现了RedisRateLimiter。

###### Zuul和Gateway的区别

相同点：

1、底层都是servlet

2、两者均是web网关，处理的是http请求

不同点：

1、内部实现：

　　gateway对比zuul多依赖了spring-webflux，在spring的支持下，功能更强大，内部实现了限流、负载均衡等，扩展性也更强，但同时也限制了仅适合于Spring Cloud套件
　　zuul则可以扩展至其他微服务框架中，其内部没有实现限流、负载均衡等。
2、是否支持异步
　　zuul仅支持同步
　　gateway支持异步。理论上gateway则更适合于提高系统吞吐量（但不一定能有更好的性能），最终性能还需要通过严密的压测来决定
3、框架设计的角度
　　gateway具有更好的扩展性，并且其已经发布了2.0.0的RELESE版本，稳定性也是非常好的
4、性能
　　WebFlux 模块的名称是 spring-webflux，名称中的 Flux 来源于 Reactor 中的类 Flux。Spring webflux 有一个全新的非堵塞的函数式 Reactive Web 框架，可以用来构建异步的、非堵塞的、事件驱动的服务，在伸缩性方面表现非常好。使用非阻塞API。 Websockets得到支持，并且由于它与Spring紧密集成，所以将会是一个更好的 开发 体验。
　　Zuul 1.x，是一个基于阻塞io的API Gateway。Zuul已经发布了Zuul 2.x，基于Netty，也是非阻塞的，支持长连接，但Spring Cloud暂时还没有整合计划。

##### 消息总线-Spring Cloud Bus

**管理和广播分布式系统中的消息**，也就是消息引擎系统中的广播模式。

##### 调用过程

#### 4、SpringCloud与Dubbo的区别

1. 生态环境不同：SpringCloud依托于Spring平台，具备更加完善的生态体系；而Dubbo一开始只是做RPC远程调用，生态相对匮乏，现在逐渐丰富起来。
2. 调用方式：SpringCloud是采用Http协议做远程调用，接口一般是Rest风格，比较灵活；Dubbo是采用Dubbo协议，接口一般是Java的Service接口，格式固定。但调用时采用Netty的NIO方式，性能较好。
3. 组件差异比较多，例如SpringCloud注册中心一般用Eureka，而Dubbo用的是Zookeeper

#### 5、ZooKeeper与Eureka区别

1、**ZooKeeper保证的是CP,Eureka保证的是AP**
ZooKeeper在选举期间注册服务瘫痪,虽然服务最终会恢复,但是选举期间不可用的
Eureka各个节点是平等关系,只要有一台Eureka就可以保证服务可用,而查询到的数据并不是最新的
自我保护机制会导致Eureka不再从注册列表移除因长时间没收到心跳而应该过期的服务，Eureka仍然能够接受新服务的注册和查询请求,但是不会被同步到其他节点(集群实现高可用性)，当网络稳定时,当前实例新的注册信息会被同步到其他节点中(最终一致性)
Eureka可以很好的应对因网络故障导致部分节点失去联系的情况,而不会像ZooKeeper一样使得整个注册系统瘫痪
2、**ZooKeeper有Leader和Follower角色,Eureka各个节点平等**
3、ZooKeeper采用过半数存活原则,Eureka采用自我保护机制解决分区问题
4、Eureka本质上是一个工程,而ZooKeeper只是一个进程

### 高并发

#### Redis

##### 高性能原因

1、纯内存访问，Redis将所有数据放在内存中，内存的响应时间大约为100纳秒，这时Redis达到每秒万级别访问的重要基础；

2、非阻塞I/O，Redis使用epoll作为I/O多路复用技术的实现，在加上Redis自身的事件处理模型将epoll中的链接、读写、关闭都转换为事件，不在网络I/O上浪费过多的时间；

3、单线程**避免了线程切换和竞态产生的消耗**。

In a word，**纯内存存储、IO多路复用技术（epoll技术）、单线程架构**是造就Redis高性能的三个因素。

##### 缓存常用的3种读写策略 

1. Cache Aside Pattern（旁路缓存模式）

   **写** ：

   - 先更新 DB
   - 然后直接删除 cache 。

   **读** :

   - 从 cache 中读取数据，读取到就直接返回
   - cache中读取不到的话，就从 DB 中读取数据返回
   - 再把数据放到 cache 中。

2. Read/Write Through Pattern（读写穿透）

   **写（Write Through）：**

   - 先查 cache，cache 中不存在，直接更新 DB。

   - cache 中存在，则先更新 cache，然后 cache 服务自己更新 DB（**同步更新 cache 和 DB**）。

     **先删除 cache ，后更新 DB**会造成**数据库（DB）和缓存（Cache）数据不一致**的问题

   **读(Read Through)：**

   - 从 cache 中读取数据，读取到就直接返回 。
   - 读取不到的话，先从 DB 加载，写入到 cache 后返回响应。

3. Write Behind Pattern（异步缓存写入）

   **Read/Write Through 是同步更新 cache 和 DB，而 Write Behind Caching 则是只更新缓存，不直接更新 DB，而是改为异步批量的方式来更新 DB。**

   优点：写性能非常高，非常适合一些数据经常变化又对数据一致性要求没那么高的场景，比如浏览量、点赞量

##### 缓存一致性问题

强一致性同步成本太高，如果追求强一致，那么没必要用缓存了，直接用mysql即可。通常考虑的，都是**最终一致性**。

- 我们能放入缓存的数据本就不应该是实时性、一致性要求超高的。所以缓存数据的时候**加上过期时间**，保证每天拿到当前最新数据即可。 
- 我们不应该过度设计，增加系统的复杂性 。**双写**（先修改数据库再改Redis）、**单写**模式（先写数据库再删Redis），有双写后为什么还要有单写，是怕数据库写成功但是Redis更新失败的情况
- 遇到实时性、一致性要求高的数据，就应该查数据库，即使慢点。
- 修改数据时使用**异步延迟删除缓存**

##### 分布式锁实现原理

基于Redis实现的分布式锁常用的框架是**Redisson**

**加锁**就是用“**exists myLock**”命令判断一下，如果你要加锁的那个key不存在，就可以进行加锁，加锁是一个**原子操作**

释放锁：每次释放锁对加锁次数减1，如果加锁次数为0了，说明客户端已经不再持有锁了，此时就会用“**del MyLock**”命令，从redis里删除了这个key。然后其他客户端就可以尝试完成加锁了。

锁判断：先看锁是否存在，再看是否是同一客户端，都不是就查询**剩余生存时间**进入死循环不断尝试加锁

###### watch dog自动延期机制

 客户端A加锁的锁key默认生存时间只有30秒，如果超过了30秒，客户端A还想一直持有这把锁，怎么办？其实只要客户端A一旦加锁成功，就会启动一个watch dog看门狗，**它是一个后台线程，会每隔10秒检查一下**，如果客户端A还持有锁key，那么就会不断的延长锁key的生存时间。

###### 可重入加锁机制

“exists myLock”会判断对应key的锁是否已经存在，如果存在继续判断对应的客户端ID，如果是同一客户端就对加锁次数加1

##### redlock分布式锁：**有效防止单点故障**

1. 安全特性：互斥访问，即永远只有一个 client 能拿到锁
2. 避免死锁：最终 client 都可能拿到锁，不会出现死锁的情况，即使原本锁住某资源的 client crash 了或者出现了网络分区
3. 容错性：只要大部分 Redis 节点存活就可以正常提供服务

实现原理：

 1、获取当前时间
 2、依次N个节点获取锁，并设置响应超时时间，防止单节点获取锁时间过长
 3、锁有效时间=锁过期时间-获取锁耗费时间，如果第2步骤中获取成功的节点数大于 N/2+1,且锁有效时间大于0，则获得锁成功
 4、若获得锁失败，则向所有节点释放锁

**锁过期时间内从半双以上的节点成功获取到了锁则说明获取锁成功。这个有点像注册中心的选举机制。**

##### 集群模式

1、主从模式

 **Redis 提供了复制（replication）功能，可以实现当一台数据库中的数据更新后，自动将更新的数据同步到其他数据库上**。推+拉

- 支持主从复制，主机会自动将数据同步到从机，可以进行**读写分离**；
- 为了分载Master的读操作压力，**Slave服务器可以为客户端提供只读操作的服务，写服务仍然必须由Master来完成**；
- Slave同样可以接受其它Slaves的连接和同步请求，这样可以有效的分载Master的同步压力；
- Master Server是以非阻塞的方式为Slaves提供服务。所以在Master-Slave同步期间，客户端仍然可以提交查询或修改请求；
- Slave Server同样是以非阻塞的方式完成数据同步。在同步期间，如果有客户端提交查询请求，Redis则返回同步之前的数据；

2、哨兵模式

- 通过发送命令，让Redis服务器返回监控其运行状态，包括主服务器和从服务器；

- 当哨兵监测到master宕机，会自动将slave切换成master，然后通过**发布订阅模式**通知其他的从服务器，修改配置文件，让它们切换主机；

- 哨兵选举

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/ef44f5b2bb4743c8a746c46e8eb4f198.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5aSP5LuY5Zu9,size_20,color_FFFFFF,t_70,g_se,x_16)

3、Cluster 集群

实现了 Redis 的分布式存储，也就是说每台 Redis 节点上存储不同的内容，每个节点保存数据和整个集群状态,每个节点都和其他所有节点连接。

redis cluster 为了保证数据的高可用性，加入了主从模式，一个主节点对应一个或多个从节点，主节点提供数据存取，从节点则是从主节点拉取数据备份，当这个主节点挂掉后，就会有这个从节点选取（**选举**）一个来充当主节点，从而保证集群不会挂掉

Redis集群会将整个集群进行分slot（槽）管理。slot范围为0-16383.slot是一个编号。当存储数据时会将数据进行hashCode取值，将hash值对**16384**取余。决定该值存放在哪个服务上。

伪集群和真集群的区别

1. 伪集群是在一台服务器上提供多个服务
2. 真是集群是在多台服务器上分别提供服务

**集群的特点**

- 所有的redis节点彼此互联(PING-PONG机制),内部使用二进制协议优化传输速度和带宽。
- 节点的fail是通过集群中超过半数的节点检测失效时才生效。
- 客户端与 Redis 节点直连,不需要中间代理层.客户端不需要连接集群所有节点,连接集群中任何一个可用节点即可。

##### 主从复制的断点续传

从redis 2.8开始，就支持主从复制的断点续传，如果主从复制过程中，网络连接断掉了，那么可以接着上次复制的地方，继续复制下去，而不是从头开始复制一份

##### **数据类型**

hash、string、list、set、zset

底层数据结构：简单动态字符串、字典、列表、压缩列表、跳跃表、整数集合

**set**：是一种无序集合，集合中的元素没有先后顺序，但是**不允许重复**

**Zset**：和 set 相比，sorted set 增加了一个权重参数 score，使得集合中的元素能够按 score 进行有序排列，还可以通过 score 的范围来获取元素的列表。有点像是 Java 中 HashMap 和 TreeSet 的结合体。**使用跳表进行查询**

 **Redis 除了做缓存（高性能和高并发）之外，Redis 也经常用来做分布式锁，甚至是消息队列（zset）** 

 **Redis 是不支持 回滚（roll back） 的** 

 **Redis 还支持事务 、持久化、Lua 脚本、多种集群方案**

Redis 可以通过 **MULTI，EXEC，DISCARD 和 WATCH** 等命令来实现**事务**(transaction)功能

**Redis 是不支持 roll back（回滚） 的，因而不满足原子性的（而且不满足持久性）**

**Redis事务提供了一种将多个命令请求打包的功能。然后，再按顺序执行打包的所有命令，并且不会被中途打断。**

**pipeline**：当client 使用pipelining 发送命令时，redis server必须部分请求放到队列中（使用内存）执行完毕后一次性发送结果；如果发送的命名很多的话，建议对返回的结果加标签，当然这也会增加使用的内存；可以进行**批处理**，处理大量数据

##### 使用的代价

1. **系统复杂性增加** ：引入缓存之后，你要维护缓存和数据库的数据一致性、维护热点缓存等等。
2. **系统开发成本往往会增加** ：引入缓存意味着系统需要一个单独的缓存服务，这是需要花费相应的成本的，并且这个成本还是很贵的，毕竟耗费的是宝贵的内存。但是，如果你只是简单的使用一下本地缓存存储一下简单的数据，并且数据量不大的话，那么就不需要单独去弄一个缓存服务。

##### 删除策略

 Redis 采用的是 **定期删除+惰性/懒汉式删除** 

1. **惰性删除** ：只会在取出key的时候才对数据进行过期检查。这样对CPU最友好，但是可能会造成太多过期 key 没有被删除。
2. **定期删除** ： 每隔一段时间抽取一批 key 执行删除过期key操作。并且，Redis 底层会通过限制删除操作执行的时长和频率来减少删除操作对CPU时间的影响。

#####  内存淘汰机制

1. **volatile-lru（least recently used）**：从**已设置过期时间的数据集**执行LRU算法进行淘汰
2. **allkeys-lru（least recently used）**：当内存不足以容纳新写入数据时，**在全部空间中**，执行LRU算法进行淘汰
3. **volatile-ttl**：从已设置过期时间的数据集中挑选**将要过期**的数据淘汰
4. **volatile-random**：从已设置过期时间的数据集中**任意选择**数据淘汰
5. **allkeys-random**：在所有KEY中任意选择数据淘汰
6. **no-eviction**：禁止驱逐数据，也就是说当内存不足以容纳新写入数据时，新写入操作会报错。（少用）

4.0 版本后增加以下两种：

1. **volatile-lfu（least frequently used）**：从已设置过期时间的数据集(server.db[i].expires)中挑选**最不经常使用**的数据淘汰
2. **allkeys-lfu（least frequently used）**：当内存不足以容纳新写入数据时，在所有KEY中，执行LFU算法进行淘汰

##### LRU和LFU的区别

LRU是最近最少使用页面置换算法(Least Recently Used),也就是首先淘汰**最长时间未被使用**的页面!

LFU是最近最不常用页面置换算法(Least Frequently Used),也就是淘汰**一定时期内被访问次数最少**的页!

##### 持久化机制

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ee72734583c475ea3e4234fbb991d33~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp" alt="img" style="zoom: 67%;" />

  **快照（snapshotting）持久化（RDB）** 

 通过创建快照来获得存储在内存里面的数据在某个时间点上的副本 

 **只追加文件（ append-only file, AOF）** 

 每执行一条会**更改** Redis 中的数据的命令，Redis 就会将该命令写入硬盘中的 AOF 文件 

##### AOF重写

- AOF 重写可以产生一个新的 AOF 文件，这个新的 AOF 文件和原有的 AOF 文件所保存的数据库状态一样，但体积更小。

  AOF 重写是一个有歧义的名字，该功能是通过读取数据库中的键值对来实现的，程序无须对现有 AOF 文件进行任何读入、分析或者写入操作。

  在执行 BGREWRITEAOF 命令时，Redis 服务器会维护一个 AOF 重写缓冲区，该缓冲区会在子进程创建新 AOF 文件期间，记录服务器执行的所有写命令。当子进程完成创建新 AOF 文件的工作之后，服务器会将重写缓冲区中的所有内容追加到新 AOF 文件的末尾，使得新旧两个 AOF 文件所保存的数据库状态一致。最后，服务器用新的 AOF 文件替换旧的 AOF 文件，以此来完成 AOF 文件重写操作

![图片.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/443e6b91d921475f9304a484331ee4ac~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 缓存穿透

 大量请求的 key 根本不存在于缓存中，导致请求直接到了数据库上，根本没有经过缓存这一层。（黑客） 

###### 解决方法

 **1、缓存无效 key** 

 缓存和数据库都查不到某个 key 的数据就写一个到 Redis 中去并设置过期时间 ，时间可以短些

 **2、布隆过滤器** 

 把**所有可能存在的请求**的值都存放在布隆过滤器中，当用户请求过来，先判断用户发来的请求的值是否存在于布隆过滤器中。不存在的话，直接返回请求参数错误信息给客户端，存在的话才会走下面的流程 

**布隆过滤器说某个元素存在，小概率会误判。布隆过滤器说某个元素不在，那么这个元素一定不在。**

**当一个元素加入布隆过滤器中的时候，会进行哪些操作：**

1. 使用布隆过滤器中的哈希函数对元素值进行计算，得到哈希值（有几个哈希函数得到几个哈希值）。
2. 根据得到的哈希值，在位数组中把对应下标的值置为 1。

**当我们需要判断一个元素是否存在于布隆过滤器的时候，会进行哪些操作：**

1. 对给定元素再次进行相同的哈希计算；
2. 得到值之后判断位数组中的每个元素是否都为 1，如果值都为 1，那么说明这个值在布隆过滤器中，如果存在一个值不为 1，说明该元素不在布隆过滤器中。

一定会出现这样一种情况：**不同的字符串可能哈希出来的位置相同。** （可以适当增加位数组大小或者调整我们的哈希函数来降低概率）

##### 缓存雪崩

 缓存在同一时间大面积的**失效**，后面的请求都直接落到了数据库上，造成数据库短时间内承受大量请求

**针对 Redis 服务不可用的情况：**

1. 采用 Redis 集群，避免单机出现问题整个缓存服务都没办法使用。
2. 限流，避免同时处理大量的请求。

**针对热点缓存失效的情况：**

1. 设置不同的失效时间比如随机设置缓存的失效时间。
2. 缓存永不失效。

##### 缓存击穿

原因：指缓存中没有但数据库中有的数据，由于**并发用户特别多**，同时读缓存没读到数据，又同时去数据库去取数据，引起数据库压力瞬间增大，造成过大压力

方案：热点数据永不过期，加互斥锁，用集群

#### 消息队列

**销峰、解耦、异步**

| 对比方向 | 概要                                                         |
| -------- | ------------------------------------------------------------ |
| 吞吐量   | 万级的 ActiveMQ 和 RabbitMQ 的吞吐量（ActiveMQ 的性能最差）要比 十万级甚至是百万级的 RocketMQ 和 Kafka 低一个数量级。 |
| 可用性   | 都可以实现高可用。ActiveMQ 和 RabbitMQ 都是基于主从架构实现高可用性。RocketMQ 基于分布式架构。 kafka 也是分布式的，一个数据多个副本，少数机器宕机，不会丢失数据，不会导致不可用 |
| 时效性   | RabbitMQ 基于erlang开发，所以**并发能力很强，性能极其好，延时很低**，达到微秒级。其他三个都是 ms 级。 |
| 功能支持 | 除了 Kafka，其他三个功能都较为完备。 Kafka 功能较为简单，主要支持简单的MQ功能，在大数据领域的实时计算以及日志采集被大规模使用，是事实上的标准 |
| 消息丢失 | ActiveMQ 和 RabbitMQ 丢失的可能性非常低， RocketMQ 和 Kafka 理论上不会丢失。 |

##### RabbitMQ

RabbitMQ使用**AMQP**协议



<img src="https://camo.githubusercontent.com/6ba7ff34904c9491910064f349eb85007e1a62456a7800223fd1f1caf26d9e43/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d31322d31362f39363338383534362e6a7067" alt="图1-RabbitMQ 的整体模型架构" style="zoom: 80%;" />

RabbitMQ 常用的 **Exchange Type** 有 **fanout（绑定/订阅）**、**direct（设置消息类型来绑定）**、**topic（按路由）**、**headers（消息头）** 这四种协议

direct：（点对点）在direct类型的exchange中，只有这交换机和队列的routingkey完全相同，exchange才会选择对应的binging进行消息路由。

topic：和上面的direct类型差不多，但direct类型要求routingkey完全相等，这里的routingkey可以有通配符：'*','#'.

fanout：（广播）此exchange的路由规则很简单直接将消息路由到所有绑定的队列中，无须对消息的routingkey进行匹配操作。

header：此类型的exchange和以上三个都不一样，其路由的规则是根据header来判断

###### RabbitMQ fanout广播消息使用匿名队列

广播模式，发送的消息被所有绑定到这个交换机的所有队列消费到，但是**队列名称不固定**

默认情况下，队列名称以spring.gen-为前缀，后跟UUID的base64表示形式

###### 消息的顺序性

- 拆分多个queue，每个queue一个consumer，就是多一些queue而已，确实是麻烦点；
- 一个queue但是对应一个consumer，然后这个consumer内部用内存队列做排队，然后分发给底层不同的worker来处理

###### 实现延迟消息

1、使用插件来实现（rabbitmq-delayed-message-exchange）

2、建立2个队列，一个用于发送消息，一个用于消息过期后的转发目标队列。生产者输出消息到Queue1，并且这个消息是设置有有效时间的，比如60s。消息会在Queue1中等待60s，如果没有消费者收掉的话，它就是被转发到Queue2，Queue2有消费者，收到，处理延迟任务

###### 消息丢失

1、生产者丢失

	1）可以选择用rabbitmq提供的**事务功能**
	
	2）可以**开启confirm模式**，确认成功后返回ack消息

2、mq丢失

	开启**mq持久化**，写入磁盘，queue的持久化是通过durable=true来实现的。

3、消费者丢失

	可以**关闭自动提交offset**，消费成功再提交。

###### 重复消费

RabbitMQ不保证消息不重复，如果你的业务需要保证严格的不重复消息，需要你自己在业务端去重。

1. 使用幂等操作

   乐观锁：每个数据有一个版本号，和当前版本号相同的时候进行更新

   设置唯一性索引，如果已经存在值了就不行更新

###### 消息积压

1、MQ动态扩容，将MQ容量增大，让其能容纳更多的消息，增加消费者数量

2、消费端加大消费能力，迅速处理掉积压。

若是设置了过期时间，可以写个程序查出来后期再补回去，

###### 死信队列

消费失败几次后进死信队列，可以发邮件处理，定时发送

##### Kafka

<img src="/Users/xudandan/Documents/KafkaTopicPartitioning.png" alt="Kafka Topic Partition" style="zoom: 80%;" />

Kafka 比较重要的几个概念：

1. **Producer（生产者）** : 产生消息的一方。
2. **Consumer（消费者）** : 消费消息的一方。
3. **Broker（代理）** : 可以看作是一个独立的 Kafka 实例。多个 Kafka Broker 组成一个 Kafka Cluster。

同时，你一定也注意到每个 Broker 中又包含了 Topic 以及 Partition 这两个重要的概念：

- **Topic（主题）** : Producer 将消息发送到特定的主题，Consumer 通过订阅特定的 Topic(主题) 来消费消息。
- **Partition（分区）** : Partition 属于 Topic 的一部分。一个 Topic 可以有多个 Partition ，并且同一 Topic 下的 Partition 可以分布在不同的 Broker 上，这也就表明一个 Topic 可以横跨多个 Broker 。这正如我上面所画的图一样。

使用Scala语言开发，天然具有高并发能力

kafka集群、producer、consumer都依赖**zookeeper**来保证系统可用性

不支持事务控制

**有序性保证**：**Kafka 只能为我们保证 Partition(分区) 中的消息有序。所以** **1 个 Topic 只对应一个 Partition就可以保证**

**不丢失**：生产者通过 `get()`方法获取调用结果，但是一般不推荐这么做！可以采用为其**添加回调函数**的形式。设置重试次数（大于3）

消费者**手动关闭自动提交 offset**。

配置 **acks = all** 代表则所有副本都要接收到该消息之后该消息才算真正成功被发送。

**不重复消费**：幂等校验，将 **`enable.auto.commit`** 参数设置为 false，关闭自动提交

**大数据使用，支持高并发，动态扩容，支持文件存储**

https://blog.csdn.net/qq_28900249/article/details/90346599

##### ActiveMQ

支持很多协议

#### 分库分表

分库分表是为了解决由于库、表数据量过大，而导致数据库性能持续下降的问题。

**hash取模**判断放在什么位置

先垂直分，再水平分

先分表，再分库

事务一致性问题：事务补偿机制

排序问题：需要先在不同的分片节点中将数据进行排序并返回，然后将不同分片返回的结果集进行汇总和再次排序，最终返回

全局唯一主键问题：全局唯一ID就叫分布式ID

#### 读写分离

将数据库的读和写操作分不到不同的数据库节点上。主服务器负责写，从服务器负责读。另外，一主一从或者一主多从都可以。

#### 负载均衡

##### DNS 负载均衡

一般用来实现地理级别的均衡

##### 硬件负载均衡 F5

通过单独的硬件设备比如 F5 来实现负载均衡功能

##### 软件负载均衡Nginx

通过负载均衡软件比如 Nginx 来实现负载均衡功能，Nginx-反向代理服务器

Nginx采用了Linux的epoll模型，epoll模型基于事件驱动机制，它可以监控多个事件是否准备完毕，如果OK，那么放入epoll队列中，这个过程是异步的。worker只需要从epoll队列循环处理即可。

**Keepalived+Nginx实现高可用**。

思路：

第一：请求不要直接打到Nginx上，应该先通过Keepalived（这就是所谓虚拟IP，VIP）

第二：Keepalived应该能监控Nginx的生命状态（提供一个用户自定义的脚本，定期检查Nginx进程状态，进行权重变化，从而实现Nginx故障切换）

##### Nginx负载均衡算法：

- 随机（可加权）
- 轮训（可加权）
- 一致性Hash，相同参数的请求打到同一台服务器上
- 最小连接数

#### 高可用

一个系统在大部分时间都是可用的，可以为我们提供服务的。高可用代表**系统即使在发生硬件故障或者系统升级**的时候，服务仍然是可用的

##### CAP原理

Consistency（一致性）、Availability（可用性）、Partition Tolerance（分区容错性）

 CAP 理论中分区容错性 P(**必须的**) 是一定要满足的，在此基础上，只能满足可用性 A 或者一致性 C 

**zookeeper满足CP原理，eureka的AP原则**

##### BASE原理

Basically Available（基本可用） 、Soft-state（软状态） 和 Eventually Consistent（最终一致性） 三个短语的缩写。BASE 理论是对 CAP 中一致性和可用性权衡的结果，其来源于对大规模互联网系统分布式实践的总结，是基于 CAP 定理逐步演化而来的，它大大降低了我们对系统的要求

#### 限流

- 固定窗口计数器；
  - 将时间划分为多个窗口；
  - 在每个窗口内每有一次请求就将计数器加一；
  - 如果计数器超过了限制数量，则本窗口内所有的请求都被丢弃当时间到达下一个窗口时，计数器重置。
- 滑动窗口计数器；
  - 将时间划分为多个区间；
  - 在每个区间内每有一次请求就将计数器加一维持一个时间窗口，占据多个区间；
  - 每经过一个区间的时间，则抛弃最老的一个区间，并纳入最新的一个区间；
  - 如果当前窗口内区间的请求计数总和超过了限制数量，则本窗口内所有的请求都被丢弃。
- 漏桶；
  - 将每个请求视作"水滴"放入"漏桶"进行存储；
  - “漏桶"以固定速率向外"漏"出请求来执行如果"漏桶"空了则停止"漏水”；
  - 如果"漏桶"满了则多余的"水滴"会被直接丢弃。
- 令牌桶。**处理突发流量**
  - 令牌以固定速率生成；
  - 生成的令牌放入令牌桶中存放，如果令牌桶满了则多余的令牌会直接丢弃，当请求到达时，会尝试从令牌桶中取令牌，取到了令牌的请求可以执行；
  - 如果桶空了，那么尝试取令牌的请求会被直接丢弃。

#### 降级

降级之后返回托底数据

#### 熔断

**当失败率达到阀值自动触发降级**(如因网络故障/超时造成的失败率高)，熔断器触发的快速失败会进行快速恢复。

#### 排队

#### 集群

#### 超时和重试机制

## 三、多线程

### 线程创建方式

 1.继承 Thread 类，重写run方法，调用start方法;

 2.实现 Runnable 接口，重写run方法，调用Thread的构造，调用start方法;

 3.使用 FutureTask 

 4.使用 Executor 框架（线程池）

### 线程、程序、进程的基本概念

**线程**与进程相似，但线程是一个比进程更小的执行单位。一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的多个线程共享同一块内存空间和一组系统资源，所以系统在产生一个线程，或是在各个线程之间作切换工作时，负担要比进程小得多，也正因为如此，线程也被称为轻量级进程。

**程序**是含有指令和数据的文件，被存储在磁盘或其他的数据存储设备中，也就是说程序是静态的代码。

**进程**是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。系统运行一个程序即是一个进程从创建，运行到消亡的过程。简单来说，一个进程就是一个执行中的程序，它在计算机中一个指令接着一个指令地执行着，同时，每个进程还占有某些系统资源如 CPU 时间，内存空间，文件，输入输出设备的使用权等等。换句话说，当程序在执行时，将会被操作系统载入内存中。 线程是进程划分成的更小的运行单位。线程和进程最大的不同在于基本上各进程是独立的，而各线程则不一定，因为同一进程中的线程极有可能会相互影响。从另一角度来说，进程属于操作系统的范畴，主要是同一段时间内，可以同时执行一个以上的程序，而线程则是在同一程序内几乎同时执行一个以上的程序段。

### 并发与并行

- **并发：** 同一时间段，多个任务都在执行 (单位时间内不一定同时执行)；
- **并行：** 单位时间内，多个任务同时执行。

### 并发编程的三个重要特性

1. **原子性** : 一个的操作或者多次操作，要么所有的操作全部都得到执行并且不会收到任何因素的干扰而中断，要么所有的操作都执行，要么都不执行。可以使用**锁**来保证原子性，在 Java 中 synchronized 和在 lock(ReentrantLock)、unlock 中操作保证原子性。使用原子类。另一种就是使用CAS来保证原子性
2. **可见性** ：当一个变量对共享变量进行了修改，那么另外的线程都是立即可以看到修改后的最新值。在 Java 中 **volatile、synchronized 和 final** 实现可见性
3. **有序性** ：代码在执行的过程中的先后顺序，Java 在编译器以及运行期间的优化，代码的执行顺序未必就是编写代码时候的顺序。Java 语言提供了 **volatile 和 synchronized** 两个关键字来保证线程之间操作的有序性。`volatile` 关键字可以禁止指令进行重排序优化。

### CAS

原理：

1. 自旋锁
2. Unsafe类，所有方法都是native修饰，直接调用操作系统，里面的变量使用volatile修饰。

缺点：ABA问题、自旋开销大、只能保证一个共享变量的安全

### Atomic 原子类

 一个操作是不可中断的。即使是在多个线程一起执行的时候，一个操作一旦开始，就不会被其他线程干扰 

**使用CAS去控制**

**基本类型**

使用原子的方式更新基本类型

- AtomicInteger：整形原子类
- AtomicLong：长整型原子类
- AtomicBoolean：布尔型原子类

**数组类型**

使用原子的方式更新数组里的某个元素

- AtomicIntegerArray：整形数组原子类
- AtomicLongArray：长整形数组原子 类
- AtomicReferenceArray：引用类型数组原子类

**引用类型**

- AtomicReference：引用类型原子类
- AtomicStampedReference：原子更新引用类型里的字段原子类
- AtomicMarkableReference ：原子更新带有标记位的引用类型

**对象的属性修改类型**

- AtomicIntegerFieldUpdater：原子更新整形字段的更新器
- AtomicLongFieldUpdater：原子更新长整形字段的更新器
- AtomicStampedReference：原子更新带有版本号的引用类型。该类将整数值与引用关联起来，可用于解决原子的更新数据和数据的版本号，可以解决使用 CAS 进行原子更新时可能出现的 ABA 问题。

### 线程状态

<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/19-1-29/Java%E7%BA%BF%E7%A8%8B%E7%9A%84%E7%8A%B6%E6%80%81.png" alt="Java线程的状态" style="zoom: 80%;" />

Java 线程状态变迁

<img src="https://camo.githubusercontent.com/9b25cbe08239220fce6606a1d8755c1361ad3c96f90e76887b582d4ed7e453c5/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31392d312d32392f4a6176612b2545372542412542462545372541382538422545372538412542362545362538302538312545352538462539382545382542462538312e706e67" alt="Java 线程状态变迁 " style="zoom: 80%;" />

注：一个线程start()了两次会抛异常，报非法的线程状态

线程启动前会检查线程状态，默认0，启动后会改成非0

### Runnable和Callable接口的区别

1.**Callable可以返回一个类型V，而Runnable不可以**
2.**Callable能够抛出checked exception,而Runnable不可以**。
3.Runnable是自从java1.1就有了，而Callable是1.5之后才加上去的
4.**Callable和Runnable都可以应用于executors。而Thread类只支持Runnable**.
上面只是简单的不同，其实这两个接口在用起来差别还是很大的。Callable与executors联合在一起，在任务完成时可立刻获得一个更新了的Future。而Runable却要自己处理

#### wait/notify 与 park/unpark

- wait，notify和notifyAll必须配合Object Monitor一起使用，而unpark不必
- park & unpark是以线程为单位来【阻塞】和【唤醒】线程，而notify只能随机唤醒一个等待线程，
  notifyAll是唤醒所有等待线程，就不那么【精确】
- park & unpark可以先unpark，而wait & notify不能先notify

#### 等待池与锁池

- 等待池：假设一个线程A调用了某个对象的wait()方法，线程A就会释放该对象的锁后，进入到了该对象的等待池，等待池中的线程不会去竞争该对象的锁。
- 锁池：只有获取了对象的锁，线程才能执行对象的 synchronized 代码，对象的锁每次只有一个线程可以获得，其他线程只能在锁池中等待

notify() 方法随机唤醒对象的等待池中的一个线程，进入锁池；notifyAll() 唤醒对象的等待池中的所有线程，进入锁池。

### 锁

#### 悲观锁乐观锁

**悲观锁**

**总是假设最坏的情况，每次去拿数据的时候都认为别人会修改**，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁（共享资源每次只给一个线程使用，其它线程阻塞，用完后再把资源转让给其它线程）。传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。Java中synchronized和ReentrantLock等独占锁就是悲观锁思想的实现。

**乐观锁**

**总是假设最好的情况，每次去拿数据的时候都认为别人不会修改**，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号机制和CAS算法实现。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于write_condition机制，其实都是提供的乐观锁。在Java中java.util.concurrent.atomic包下面的原子变量类就是使用了乐观锁的一种实现方式CAS实现的。

**乐观锁一般会使用版本号机制或CAS算法实现。**

**使用场景**

**乐观锁适用于写比较少的情况下（多读场景）**，即冲突真的很少发生的时候，这样可以省去了锁的开销，加大了系统的整个吞吐量。但如果是多写的情况，一般会经常产生冲突，这就会导致上层应用会不断的进行retry，这样反倒是降低了性能，所以一般**多写的场景下用悲观锁就比较合适。**

**CAS与synchronized的使用情景**

简单的来说CAS适用于写比较少的情况下（多读场景，冲突一般较少）

synchronized适用于写比较多的情况下（多写场景，冲突一般较多）

#### 死锁

##### 具备条件

1. 互斥条件：该资源任意一个时刻只由一个线程占用。
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3. 不剥夺条件:线程已获得的资源在末使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。
4. 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

##### 如何避免死锁

1. **破坏互斥条件** ：这个条件我们没有办法破坏，因为我们用锁本来就是想让他们互斥的（临界资源需要互斥访问）。
2. **破坏请求与保持条件** ：一次性申请所有的资源。
3. **破坏不剥夺条件** ：占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。
4. **破坏循环等待条件** ：靠按序申请资源来预防。按某一顺序申请资源，释放资源则反序释放。破坏循环等待条件。

#### sleep() 方法和 wait() 方法

- 两者最主要的区别在于：**sleep 方法没有释放锁，而 wait 方法释放了锁** 。
- 两者都可以暂停线程的执行。
- Wait 通常被用于线程间交互/通信，sleep 通常被用于暂停执行。
- wait() 方法被调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 notify() 或者 notifyAll() 方法。sleep() 方法执行完成后，线程会自动苏醒。或者可以使用 wait(long timeout)超时后线程会自动苏醒。

虚假唤醒：多线程环境下，有多个线程执行了wait()方法，需要其他线程执行notify()或者notifyAll()方法去唤醒它们，假如多个线程都被唤醒了，但是只有其中一部分是有用的唤醒操作，其余的唤醒都是无用功；对于不应该被唤醒的线程而言，便是虚假唤醒。

程序仅使用**if**对程序做了一次判断，我们应该使用while循环去判断。即wait()要在**while**循环中。

#### synchronized

**`synchronized` 关键字解决的是多个线程之间访问资源的同步性，`synchronized`关键字可以保证被它修饰的方法或者代码块在任意时刻只能有一个线程执行。**

在使用 synchronized 来同步代码块的时候，经编译后，会在代码块的起始位置插入 **monitorEnter指令**，在结束或异常处插入 **monitorExit指令。**当执行到 monitorEnter 指令时，将会尝试获取对象所对应的 **monitor **的所有权，即尝试获得对象的锁。而 synchronized 用的锁是存放在 **Java对象头** 中的。

每个锁对象会有一个计数器记录线程获取几次锁，在执行完同步代码块时，计数器的数量会-1，直到计数器的数量为0，就释放这个锁。

另外，在 Java 早期版本中，`synchronized` 属于 **重量级锁**，效率低下。

JDK1.6 对锁的实现引入了大量的优化，如自旋锁、适应性自旋锁、锁消除、锁粗化、偏向锁、轻量级锁等技术来减少锁操作的开销。

可以保证方法或者代码块在运行时，同一时刻只有一个方法可以进入到临界区，同时它还可以保证共享变量的内存可见性 

**锁的四种状态：无锁->偏向锁->轻量级锁->重量级锁**

**偏向锁**是指当一段同步代码一直被同一个线程所访问时，即不存在多个线程的竞争时，那么该线程在后续访问时便会自动获得锁，从而降低获取锁带来的消耗，即提高性能。**偏向某个线程**

**轻量级锁**是指**当锁是偏向锁的时候，却被另外的线程所访问，此时偏向锁就会升级为轻量级锁**，其他线程会通过 CAS 操作和自旋的形式尝试获取锁，线程不会阻塞，从而提高性能

**重量级锁**是指当有一个线程获取锁之后，其余所有等待获取该锁的线程都会处于阻塞状态。

#### 自旋锁、适应性自旋锁

自旋的次数不在固定，而是由前一次在同一个锁上的自旋时间和锁的拥有者的状态共同决定，避免浪费处理器资源

JDK8后优化：

- 开始的时候是乐观锁，如果锁冲突频繁就转成悲观锁
- 开始的是轻量级锁，如果被持有的时间较长就转成重量级锁
- 实现轻量级锁大概率用到自旋锁策略
- 不公平锁
- 可重入锁
- 不是读写锁

 Java中每一个对象都可以作为锁，这是实现同步的基础：

1. **修饰实例方法:** 作用于当前对象实例加锁，进入同步代码前要获得 **当前对象实例的锁**

2. **修饰静态方法:** 也就是给当前类加锁，会作用于类的所有对象实例 ，进入同步代码前要获得 **当前 class 的锁**。因为静态成员不属于任何一个实例对象，是类成员

3. **修饰代码块** ：指定加锁对象，对给定对象/类加锁。`synchronized(this|object)` 表示进入同步代码库前要获得**给定对象的锁**。`synchronized(类.class)` 表示进入同步代码前要获得 **当前 class 的锁** 

#### 可重入锁

可重入就是说某个线程已经获得某个锁，可以再次获取锁而不会出现死锁

加锁几次就需要解锁几次不然会出现死锁

#### synchronized 和 ReentrantLock 的区别

两者都是**可重入锁**

synchronized 依赖于 JVM 而 ReentrantLock 依赖于 API

ReentrantLock 比 synchronized 增加了一些高级功能，如 **等待可中断**（避免出现死锁） ， **可实现公平锁** ， **可实现选择性通知（锁可以绑定多个条件Condition）** 

**公平锁**：表示线程获取锁的顺序是按照**加锁的顺序**来分配的，及先来先得，先进先出的顺序。公平锁在获取锁时会判断**阻塞队列**里是否有线程在等待，若有则获取锁就会失败，并且会加入阻塞队列。
**非公平锁**：表示获取锁的抢占机制，是随机获取锁的，和公平锁不一样的就是先来的不一定能拿到锁，有可能一直拿不到锁，所以结果不公平。

Java中**线程通信协作**的最常见的两种方式：

1、syncrhoized加锁的线程的Object类的wait()/notify()/notifyAll()

2、ReentrantLock类加锁的线程的Condition类的await()/signal()/signalAll()

#### ThreadLocal

是一种特殊的变量，是一个线程级别变量，每一个线程都有一个 独立的变量，不存在竞争，在并发模式下绝对安全的变量

#### ThreadLocal和Synchronized

**ThreadLocal**提供了**线程内存储变量**的能力，这些变量不同之处在于每一个线程读取的变量是对应的互相独立的。通过get和set方法就可以得到当前线程对应的值。

ThreadLocal的静态内部类ThreadLocalMap为每个Thread都维护了一个数组table，ThreadLocal确定了一个数组下标，而这个下标就是value存储的对应位置。

都是为了解决多线程中相同变量的访问冲突问题，不同的点是

- Synchronized是通过线程等待，牺牲时间来解决访问冲突
- ThreadLocal是通过每个线程单独一份存储空间，牺牲空间来解决冲突，并且相比于Synchronized，ThreadLocal具有线程隔离的效果，只有在线程内才能获取到对应的值，线程外则不能访问到想要的值。

**安全隐患：ThreadLocalMap中的Entry的key使用的是ThreadLocal对象的弱引用**，在没有其他地方对ThreadLoca依赖，ThreadLocalMap中的ThreadLocal对象就会被回收掉，但是对应的value不会被回收，这个时候Map中就可能存在key为null但是value不为null的项，这需要实际的时候使用完毕及时调用remove方法避免内存泄漏。

####  volatile 

 **除了防止 JVM 的指令重排 ，还有一个重要的作用就是保证变量的可见性** 

**volatile不是保护线程安全的。它保护的是变量安全。**

#### 让线程之间顺序执行

使用   **join、CountDownLatch、线程池**

#### 线程中断

不推荐使用stop，不安全也不受提倡

1、使用**退出标志位**

2、使用**Thread.interrupt()**方法，作用是中断线程。将会设置该线程的中断状态位，即设置为true，中断的结果线程是死亡、还是等待新的任务或是继续运行至下一步，就取决于这个程序本身。线程会不时地检测这个中断标示位，以判断线程是否应该被中断（中断标示值是否为true）。它并不像stop方法那样会中断一个正在运行的线程　

　　interrupt()方法只是改变中断状态，不会中断一个正在运行的线程。需要用户自己去监视线程的状态为并做处理。支持线程中断的方法（也就是线程中断后会抛出interruptedException的方法）就是在监视线程的中断状态，一旦线程的中断状态被置为“中断状态”，就会抛出中断异常。这一方法实际完成的是，给受阻塞的线程发出一个中断信号，这样受阻线程检查到中断标识，就得以退出阻塞的状态。 

  更确切的说，如果线程被Object.wait, Thread.join和Thread.sleep三种方法之一阻塞，此时调用该线程的interrupt()方法，那么该线程将抛出一个 InterruptedException中断异常（该线程必须事先预备好处理此异常），从而提早地终结被阻塞状态。如果线程没有被阻塞，这时调用 interrupt()将不起作用，直到执行到wait(),sleep(),join()时,才马上会抛出 InterruptedException。

3、利用**Future**，可以把任务封装成一个Future，Future中有一个方法“boolean cancel(boolean mayInterruptIfRunning);”如果参数为true并且任务正在某个线程中执行，那么这个线程就能够被中断，如果参数为false则表示如果任务还没有运行那就不要运行（有些任务不处理中断）。

####  synchronized和 volatile 的区别

`synchronized` 关键字和 `volatile` 关键字是两个互补的存在，而不是对立的存在！

- **`volatile` 关键字**是线程同步的**轻量级实现**，所以**`volatile `性能肯定比`synchronized`关键字要好**。但是**`volatile` 关键字只能用于变量而 `synchronized` 关键字可以修饰方法以及代码块**。
- **`volatile` 关键字能保证数据的可见性，但不能保证数据的原子性。`synchronized` 关键字两者都能保证。**
- **`volatile`关键字主要用于解决变量在多个线程之间的可见性，而 `synchronized` 关键字解决的是多个线程之间访问资源的同步性。**

#### 锁的四种状态

 无锁状态、偏向锁状态、轻量级锁状态、重量级锁状态 

 会随着竞争的激烈而逐渐升级。注意锁可以升级不可降级，这种策略是为了提高获得锁和释放锁的效率。 

#### 锁的相关技术

##### 自旋锁

 背景：互斥同步对性能最大的影响是阻塞，挂起和恢复线程都需要转入内核态中完成；并且通常情况下，共享数据的锁定状态只持续很短的一段时间，为了这很短的一段时间进行上下文切换并不值得。

原理：当一条线程需要请求一把已经被占用的锁时，并不会进入阻塞状态，而是继续持有CPU执行权等待一段时间，该过程称为『自旋』。继续运行一段无效代码。自旋默认次数是10次。

优点：由于自旋等待锁的过程线程并不会引起上下文切换，因此比较高效；

缺点：自旋等待过程线程一直占用CPU执行权但不处理任何任务，因此若该过程过长，那就会造成CPU资源的浪费。

**自适应自旋锁**：自适应自旋可以根据以往自旋等待时间的经验，计算出一个较为合理的本次自旋等待时间。

##### 锁消除

 JVM检测到不可能存在共享数据竞争，这是JVM会对这些同步锁进行锁消除 

##### 锁粗化

 就是将多个连续的加锁、解锁操作连接在一起，扩展成一个范围更大的锁 

##### 轻量级锁 

本质：使用CAS取代互斥同步。

背景：『轻量级锁』是相对于『重量级锁』而言的，而重量级锁就是传统的锁。

轻量级锁与重量级锁的比较：  

- 重量级锁是一种悲观锁，它认为总是有多条线程要竞争锁，所以它每次处理共享数据时，不管当前系统中是否真的有线程在竞争锁，它都会使用互斥同步来保证线程的安全；
- 而轻量级锁是一种乐观锁，它认为锁存在竞争的概率比较小，所以它不使用互斥同步，而是使用CAS操作来获得锁，这样能减少互斥同步所使用的『互斥量』带来的性能开销。

实现原理：  

- 对象头称为『Mark Word』，虚拟机为了节约对象的存储空间，对象处于不同的状态下，Mark Word中存储的信息也所有不同。
- Mark Word中有个标志位用来表示当前对象所处的状态。
- 当线程请求锁时，若该锁对象的Mark Word中标志位为01（未锁定状态），则在该线程的栈帧中创建一块名为『锁记录』的空间，然后将锁对象的Mark Word拷贝至该空间；最后通过CAS操作将锁对象的Mark Word指向该锁记录；
- 若CAS操作成功，则轻量级锁的上锁过程成功；
- 若CAS操作失败，再判断当前线程是否已经持有了该轻量级锁；若已经持有，则直接进入同步块；若尚未持有，则表示该锁已经被其他线程占用，此时轻量级锁就要膨胀成重量级锁。

前提：轻量级锁比重量级锁性能更高的前提是，在轻量级锁被占用的整个同步周期内，不存在其他线程的竞争。若在该过程中一旦有其他线程竞争，那么就会膨胀成重量级锁，从而除了使用互斥量以外，还额外发生了CAS操作，因此更慢！ 

##### 偏向锁

 作用：偏向锁是为了消除无竞争情况下的同步原语，进一步提升程序性能。

与轻量级锁的区别：轻量级锁是在无竞争的情况下使用CAS操作来代替互斥量的使用，从而实现同步；而偏向锁是在无竞争的情况下完全取消同步。

与轻量级锁的相同点：它们都是乐观锁，都认为同步期间不会有其他线程竞争锁。

原理：当线程请求到锁对象后，将锁对象的状态标志位改为01，即偏向模式。然后使用CAS操作将线程的ID记录在锁对象的Mark Word中。以后该线程可以直接进入同步块，连CAS操作都不需要。但是，一旦有第二条线程需要竞争锁，那么偏向模式立即结束，进入轻量级锁的状态。

优点：偏向锁可以提高有同步但没有竞争的程序性能。但是如果锁对象时常被多条线程竞争，那偏向锁就是多余的。

偏向锁可以通过虚拟机的参数来控制它是否开启。

##### 重量级锁

 重量级锁通过对象内部的监视器（monitor）实现，其中monitor的本质是依赖于底层操作系统的Mutex Lock实现，操作系统实现线程之间的切换需要从用户态到内核态的切换，切换成本非常高 

### 线程池

#### 线程池原理

预先启动一些线程，线程无限循环从任务队列中获取一个任务进行执行，直到线程池被关闭。如果某个线程因为执行某个任务发生异常而终止，那么重新创建一个新的线程而已，如此反复。

线程池是什么时候创建线程的？

*任务提交的时候*

#### 使用线程池的好处

- **降低资源消耗**。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。
- **提高响应速度**。当任务到达时，任务可以不需要的等到线程创建就能立即执行。
- **提高线程的可管理性**。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

#### 如何实现

1. 创建线程池对象(Executors)
2. 创建Runnable/Callable接口子类对象
3. 提交子类对象，submit/execute
4. 关闭线程池

使用 ThreadPoolExecutor  （ 不建议使用 Executors 去创建 ，可能导致OOM（内存溢出））

**FixedThreadPool**：只有核心线程，且数量固定，没有非核心线程。keepAliveTime设置为0L，代表多余的线程会被立即终止。因为不会产生多余的线程，所以keepAliveTime是无效的参数；任务队列采用了无界的阻塞队列LinkedBlockingQueue（容量默认为Integer.MAX_VALUE)

**SingleThreadExecutor** : corePoolSize 和 maximumPoolSize 被 设 置 为 1,使用无界 队 列 LinkedBlockingQueue作为线程池的工作队列（ 队 列的容量 为 Integer.MAX_VALUE ）

**CachedThreadPool** corePoolSize = 0，maximumPoolSize设置为Integer.MAX_VALUE，代表没有核心线程，非核心线程是无界的；keepAliveTime = 60L，空闲线程等待新任务的最长时间是60s；用了阻塞队列SynchronousQueue,是一个不存储元素的阻塞队列，每一个插入操作必须等待另一个线程的移除操作，同理一个移除操作也得等待另一个线程的插入操作完成

#### 线程池带来的问题

 内存泄漏、死锁、线程不安全 等

#### execute()方法和submit()方法的区别

1)execute() 方法用于提交**不需要返回值**的任务，所以无法判断任务是否被线程池执行成功与否；

2)submit() 方法用于提交**需要返回值**的任务。线程池会返回一个Future类型的对象，通过这个Future对象可以判断任务是否执行成功，并且可以通过future的get()方法来获取返回值，get()方法会阻塞当前线程直到任务完成，而使用 get（long timeout，TimeUnit unit）方法则会阻塞当前线程一段时间后立即返回，这时候有可能任务没有执行完。

#### 线程池参数

![img](https://upload-images.jianshu.io/upload_images/6024478-88ee7b20f8f45825.png?imageMogr2/auto-orient/strip|imageView2/2/w/937/format/webp)

任务进来时，首先执行判断，判断核心线程是否处于空闲状态，如果不是，核心线程就先就执行任务，如果核心线程已满，则判断任务队列是否有地方存放该任务，若果有，就将任务保存在任务队列中，等待执行，如果满了，在判断最大可容纳的线程数，如果没有超出这个数量，就开创非核心线程执行任务，如果超出了，就调用handler实现拒绝策略

**一、corePoolSize 核心线程大小**
线程池中最小的线程数量，即使处理空闲状态，也不会被销毁，除非设置了allowCoreThreadTimeOut。

CPU密集型：核心线程数 = CPU核数 + 1
IO密集型：核心线程数 = CPU核数 * 2+1
注：IO密集型（某大厂实践经验）
核心线程数 = CPU核数 / （1-阻塞系数）
例如阻塞系数 0.8，CPU核数为4，则核心线程数为20

**二、maximumPoolSize 线程池最大线程数量**
一个任务被提交后，首先会被缓存到工作队列中，等工作队列满了，则会创建一个新线程，处理从工作队列中的取出一个任务。

**三、keepAliveTime 空闲线程存活时间**
当线程数量大于corePoolSize时，一个处于空闲状态的线程，在指定的时间后会被销毁。

**四、unit 空间线程存活时间单位**
keepAliveTime的计量单位

**五、workQueue就是阻塞队列**，任务可以储存在任务队列中等待被执行，执行的是FIFIO原则（先进先出），底层是BlockingQueue

**六、threadFactory 线程工厂**
创建一个新线程时使用的工厂，可以用来设定线程名、是否为daemon线程等等

**七、handler 拒绝策略**
当工作队列中的任务已满并且线程池中的线程数量也达到最大，这时如果有新任务提交进来，拒绝策略就是解决这个问题的，jdk中提供了4中拒绝策略：

	   第一种AbortPolicy:不执行新任务，直接抛出RejectedExecutionException异常，提示线程池已满（**默认**）
	
	   第二种DisCardPolicy:不执行新任务，也不抛出异常
	
	   第三种DisCardOldSetPolicy:将消息队列中的第一个任务替换为当前新进来的任务执行
	
	   第四种CallerRunsPolicy:直接调用execute来执行当前任务

#### 线程池的关闭

ThreadPoolExecutor提供了两个方法，用于线程池的关闭，分别是shutdown()和shutdownNow()，其中：

shutdown()：不会立即终止线程池，而是要等所有任务缓存队列中的任务都执行完后才终止，但再也不会接受新的任务

shutdownNow()：立即终止线程池，并尝试打断正在执行的任务，并且清空任务缓存队列，返回尚未执行的任务

#### ForkJoinPool

一种线程池，把一个大任务拆成多个小任务并行执行。注：可实现归并排序

#### FutureTask

**一个可取消的异步计算**。Future 提供了对Future的基本实现，可以调用方法去开始和取消一个计算，可以查询计算是否完成并且获取计算结果。只有当计算完成时才能获取到计算结果，一旦计算完成，计算将不能被重启或者被取消，除非调用runAndReset方法。
除了实现了Future接口以外，FutureTask还实现了Runnable接口，因此FutureTask交由Executor执行，也可以直接用线程调用执行(futureTask.run())。根据FutureTask的run方法执行的时机，FutureTask可以处于以下三种执行状态：
1、未启动：在FutureTask.run()还没执行之前，FutureTask处于未启动状态。当创建一个FutureTask对象，并且run()方法未执行之前，FutureTask处于未启动状态。
2、已启动：FutureTask对象的run方法启动并执行的过程中，FutureTask处于已启动状态。
3、已完成：FutureTask正常执行结束，或者FutureTask执行被取消(FutureTask对象cancel方法)，或者FutureTask对象run方法执行抛出异常而导致中断而结束，FutureTask都处于已完成状态。

### AQS

AQS：AbstractQuenedSynchronizer抽象的队列式同步器。

 AQS 是一个用来**构建锁和同步器**的框架，使用 AQS 能简单且高效地构造出应用广泛的大量的同步器，比如我们提到的 ReentrantLock，Semaphore（信号量），其他的诸如 ReentrantReadWriteLock，SynchronousQueue，FutureTask 等等皆是基于 AQS 的。当然，我们自己也能利用 AQS 非常轻松容易地构造出符合我们自己需求的同步器。 

用**state属性**来表示资源的状态（分独占模式和共享模式），子类需要定义如何维护这个状态，控制如何获取锁和释放锁

**AQS 定义两种资源共享方式**

- Exclusive

  （独占）：只有一个线程能执行，如 ReentrantLock。又可分为公平锁和非公平锁：

  - 公平锁：按照线程在队列中的排队顺序，先到者先拿到锁
  - 非公平锁：当线程要获取锁时，无视队列顺序直接去抢锁，谁抢到就是谁的

- **Share**（共享）：多个线程可同时执行，如 Semaphore/CountDownLatch。Semaphore、CountDownLatch、 CyclicBarrier、ReadWriteLock 。

#### ReentrantLock

**可重入锁，可实现公平锁，响应可中断**，lock()/unlock()/tryLock()/tryLock(时间,时间单位)，可以加condition，wait()，signal()

如果处于排队等候机制中的线程一直无法获取锁，线程所在节点的状态会变成取消状态，取消状态的节点会从队列中释放

AQS的Acquire会调用tryAcquire方法，tryAcquire由各个自定义同步器实现，通过tryAcquire完成加锁过程。

加锁：

通过ReentrantLock的加锁方法Lock进行加锁操作。
会调用到内部类Sync的Lock方法，由于Sync#lock是抽象方法，根据ReentrantLock初始化选择的公平锁和非公平锁，执行相关内部类的Lock方法，本质上都会执行AQS的Acquire方法。
AQS的Acquire方法会执行tryAcquire方法，但是由于tryAcquire需要自定义同步器实现，因此执行了ReentrantLock中的tryAcquire方法，由于ReentrantLock是通过公平锁和非公平锁内部类实现的tryAcquire方法，因此会根据锁类型不同，执行不同的tryAcquire。
tryAcquire是获取锁逻辑，获取失败后，会执行框架 AQS的后续逻辑，跟ReentrantLock自定义同步器无关。

解锁：

通过 ReentrantLock的解锁方法 Unlock进行解锁。
Unlock会调用内部类 Sync的 Release方法，该方法继承于AQS。
Release中会调用 tryRelease方法，tryRelease需要自定义同步器实现，tryRelease只在ReentrantLock中的Sync实现，因此可以看出，释放锁的过程，并不区分是否为公平锁。
释放成功后，所有处理由AQS框架完成，与自定义同步器无关。

#### CountDownLatch倒计数器

- countDownLatch这个类**使一个线程等待其他线程各自执行完毕后再执行。**

- 是通过一个计数器来实现的，计数器的初始值是线程的数量。每当一个线程执行完毕后，计数器的值就-1，当计数器的值为0时，表示所有线程都执行完毕，然后在闭锁上等待的线程就可以恢复工作了。

await：方法等待计数器值变为0，在这之前，线程进入等待状态

countdown：计数器值减一，直到为0

#### Semaphore信号量

常用于**限制可以访问某些资源的线程数量**，例如通过 Semaphore 限流。

Semaphore 操作：

1. 初始化
2. 增加：acquire
3. 减少：release
4. 获取可用数目：availablePermits

#### ReadWriteLock读写锁

1. Java并发库中ReetrantReadWriteLock实现了ReadWriteLock接口并添加了**可重入**的特性
2. ReetrantReadWriteLock读写锁的**效率明显高**于synchronized关键字
3. ReetrantReadWriteLock读写锁的实现中，**读锁使用共享模式；写锁使用独占模式**，换句话说，读锁可以在没有写锁的时候被多个线程同时持有，写锁是独占的
4. ReetrantReadWriteLock读写锁的实现中，需要注意的，**当有读锁时，写锁就不能获得**；而**当有写锁时，除了获得写锁的这个线程可以获得读锁外，其他线程不能获得读锁**

#### CyclicBarrier线程栅栏

创建对象时指定栅栏线程数量

await：**等指定数量的线程都处于等待状态时，继续执行后续代码**

barrierAction：线程数量到了指定量之后，自动触发执行指定任务

和CountDownLatch区别：CyclicBarrier对象可多次触发执行

使用场景：

1. 数据量比较大时，实现批量插入数据到数据库
2. 数据统计，30个线程统计30天的数据，统计完毕后执行汇总


#### CompleteFuture

java8方法，Future的实现类，异步回调返回操作结果，常用于调不同系统返回

#### CyclicBarrier和CountDownLatch的用法与区别

1. CountDownLatch的计数器只能使用一次。而CyclicBarrier的计数器可以使用reset()方法重置。所以CyclicBarrier能处理更为复杂的业务场景，比如如果计算发生错误，可以重置计数器，并让线程们重新执行一次。
2. CyclicBarrier还提供其他有用的方法，比如getNumberWaiting方法可以获得CyclicBarrier阻塞的线程数量。isBroken方法用来知道阻塞的线程是否被中断。比如以下代码执行完之后会返回true。
3. CountDownLatch会阻塞主线程，CyclicBarrier不会阻塞主线程，只会阻塞子线程。
4. 某线程中断CyclicBarrier会抛出异常，避免了所有线程无限等待。

## 四、数据库

<img src="https://upload-images.jianshu.io/upload_images/8478675-43fb20afa48907cd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp" alt="img" style="zoom:75%;" />

### 部署模式

一主

一主一从 主从复制 

一主多从 多主一从 外加haproxy代理

### 设计范式

https://www.cnblogs.com/linjiqin/archive/2012/04/01/2428695.html

#### 第一范式

第一范式是最基本的范式。如果数据库表中的**所有字段值都是不可分解的原子值**，就说明该数据库表满足了第一范式。

#### 第二范式

第二范式在第一范式的基础之上更进一层。第二范式需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）。也就是说**在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中**。

#### 第三范式

第三范式需要确保**数据表中的每一列数据都和主键直接相关，而不能间接相关**。

### 性能调优

效率低下原因：没有索引、索引失效、索引效率低、关联查询过多、产生全表扫描、死锁

#### Sql优化：

方式：性能瓶颈定位、show status命令、慢查询日志、explain分析查询、profiling分析查询

1. **SQL优化，最重要的就是优化SQL索引**，充分利用已经存在的索引，善用EXPLAIN查看SQL执行计划看索引是否起作用。
2. 数据库设计时考虑扩展性
3. 禁止跨库查询
4. 禁止使用select *
5. 避免使用子查询，使用join
6. 拆分大sql为多个小sql
7. 大数据处理分批执行
8. 优先选择符合存储的最小数据类型

#### 索引优化

###### 	设计原则

1. **最适合索引的列是在where子句中的列，或连接子句中的列，而不是出现在select关键字后的列**
2. **使用唯一索引**。考虑某列中值的分布。索引列的基数越大，效果越好（一列中相同的数据越少，索引越好）
3. **使用短索引**。如果对字符串列进行索引，应该指定一个前缀长度。这样可以节省索引空间和磁盘IO。（alter tableName add key indexName (columnName(7)) --给表tableName的columnName字段的前7位建立前缀做引，索引名字为indexName）
4. **利用最左前缀**。比如创建了一个多列索引 index_c1_c2_c3 (c1,c2,c3)，相当于创建了(c1)单列索引，(c1,c2)的组合做引以及(c1,c2,c3)的组合索引。根据这个原则，在创建多列索引时，要根据业务需求 ，where子句中使用最频繁的一列要放在索引的最左边。
5. **不要过度索引**。索引过多，会导致磁盘占用较高，insert和update操作耗时增加，查询优化效率会变低。

###### 以下不会使用索引的几种情况

1. **以%开头的like查询**
2. 数据类型出现隐式转换的不能使用索引。数据INT类型，而用varchar查询
3. 联合索引的情况下，假如查询条件不包含索引列最左边部分，不使用索引
4. 如果MySQL估计使用索引比全表扫描慢，不使用索引
5. **用or分隔开的条件**，如果or前的列中有索引，而后边的列中没有索引，不会使用索引。（or的所有条件必须全部使用索引字段才会走索引
6. **使用不等于号，is not **
7. **查询中使用函数转换**

**in通常是走索引的**，当in后面的数据在数据表中超过**30%**（上面的例子的匹配数据大约6000/16000 = 37.5%）的匹配时，会走全表扫描，即不走索引，因此in走不走索引和后面的数据有关系。

#### 选择合适的数据库存储引擎：Innodb支持行级锁

![img](https://upload-images.jianshu.io/upload_images/1780803-ac3815fe5806aef8.png?imageMogr2/auto-orient/strip|imageView2/2/w/820/format/webp)

1. 是否要支持事务，如果要请选择innodb，如果不需要可以考虑MyISAM；
2. 如果表中绝大多数都只是读查询，可以考虑MyISAM，如果既有读也有写，请使用InnoDB。
3. 系统奔溃后，MyISAM恢复起来更困难，能否接受；
4. MySQL5.5版本开始Innodb已经成为Mysql的默认引擎(之前是MyISAM)，说明其优势是有目共睹的，如果你不知道用什么，那就用InnoDB，至少不会差。

注：在Mysql中的不同的存储引擎对count函数有不同的实现方式。
**MyISAM引擎把一个表的总行数存在了磁盘上**，因此执行count(*)的时候会直接返回这个数，效率很高(没有where查询条件)。`MyISAM`表虽然count(*)很快，但是不支持事务
InnoDB引擎并没有直接将总数存在磁盘上，在执行count(*)函数的时候需要一行一行的将数据读出来，然后累计总数

**按照效率排序的话，`count(字段)`<`count(主键id)`<`count(1)`≈`count(*)`，所以建议读者，尽量使用`count(*)`。**

#### 配置优化

Sql优化：性能瓶颈定位、show status命令、慢查询日志、explain分析查询、profiling分析查询

#### B+树索引

B+树高度一般为1-3

**二叉搜索树**：二叉树，每个结点只存储一个关键字，等于则命中，小于走左结点，大于走右结点；

**B（B-）树**：多路搜索树，每个结点存储M/2到M个关键字，非叶子结点存储指向关键字范围的子结点；所有关键字在整颗树中出现，且只出现一次，非叶子结点可以命中；

**B树的每⼀个节点都包含key和value**，因此经常访问的元素可能离根节点更近，因此访问也更迅速。也会出现深度过长的问题。

**B+树**：在B-树基础上，为叶子结点增加链表指针，所有关键字都在叶子结点中出现，非叶子结点作为叶子结点的索引；B+树总是到叶子结点才命中；所以一般数据库b+深度也就3-5层

**B+树的数据都存储在叶⼦节点，非叶节点只存储索引**

**B*树**：在B+树基础上，为非叶子结点也增加链表指针，将结点的最低利用率

从1/2提高到2/3；

**B 树& B+树两者有何异同呢？**

- **B 树的所有节点既存放键(key) 也存放 数据(data)，而 B+树只有叶子节点存放 key 和 data，其他内节点只存放 key。**
- B 树的叶子节点都是独立的;B+树的叶子节点有一条引用链指向与它相邻的叶子节点。
- B 树的检索的过程相当于对范围内的每个节点的关键字做二分查找，可能还没有到达叶子节点，检索就结束了。而 B+树的检索效率就很稳定了，任何查找都是从根节点到叶子节点的过程，叶子节点的顺序检索很明显。

#### Hash索引和 B+树索引区别

**Hash索引定位快**

Hash索引指的就是Hash表，最大的优点就是能够在很短的时间内，根据Hash函数定位到数据所在的位置，这是B+树所不能比的。

**Hash冲突问题**

知道HashMap或HashTable的同学，相信都知道它们最大的缺点就是Hash冲突了。不过对于数据库来说这还不算最大的缺点。

**Hash索引不支持顺序和范围查询(Hash索引不支持顺序和范围查询是它最大的缺点。**

**B+树是有序的**，在这种**范围查询中，优势非常大**，直接遍历比500小的叶子节点就够了。而Hash索引是根据hash算法来定位的，难不成还要把 1 - 499的数据，每个都进行一次hash计算来定位吗?这就是Hash最大的缺点了。

#### 聚集索引与非聚集索引

**聚集索引**

**聚集索引即索引结构和数据一起存放的索引。主键索引属于聚集索引。**

在 Mysql 中，InnoDB引擎的表的 `.ibd`文件就包含了该表的索引和数据，对于 InnoDB 引擎表来说，该表的索引(B+树)的每个非叶子节点存储索引，叶子节点存储索引和索引对应的数据。

聚集索引的优点

聚集索引的**查询速度非常的快**，因为整个B+树本身就是一颗多叉平衡树，叶子节点也都是有序的，定位到索引的节点，就相当于定位到了数据。

聚集索引的缺点

1. **依赖于有序的数据** ：因为B+树是多路平衡树，如果索引的数据不是有序的，那么就需要在插入时排序，如果数据是整型还好，否则类似于字符串或UUID这种又长又难比较的数据，插入或查找的速度肯定比较慢。
2. **更新代价大** ： 如果对索引列的数据被修改时，那么对应的索引也将会被修改， 而且况聚集索引的叶子节点还存放着数据，修改代价肯定是较大的， 所以对于主键索引来说，主键一般都是不可被修改的。

**非聚集索引**

**非聚集索引即索引结构和数据分开存放的索引。**

**二级索引属于非聚集索引。**

> MYISAM引擎的表的.MYI文件包含了表的索引， 该表的索引(B+树)的每个叶子非叶子节点存储索引， 叶子节点存储索引和索引对应数据的指针，指向.MYD文件的数据。

**非聚集索引的叶子节点并不一定存放数据的指针， 因为二级索引的叶子节点就存放的是主键，根据主键再回表查数据。**

非聚集索引的优点

**更新代价比聚集索引要小** 。非聚集索引的更新代价就没有聚集索引那么大了，非聚集索引的叶子节点是不存放数据的

非聚集索引的缺点 

1. 跟聚集索引一样，非聚集索引也依赖于有序的数据
2. **可能会二次查询(回表)** :这应该是非聚集索引最大的缺点了。 当查到索引对应的指针或主键后，可能还需要根据指针或主键再到数据文件或表中查询。

**回表查询**，先定位主键值，再定位行记录，需要扫码两遍索引树。它的性能较扫一遍索引树更低。如在InnoDB引擎中，非主键索引查找数据时需要先找到主键，再根据主键查找具体行数据

##### 聚簇索引和非聚簇索引的区别

1. 一个表中只能拥有一个聚集索引，而非聚集索引一个表可以存在多个。
2. 索引是通过二叉树的数据结构来描述的，我们可以这么理解聚簇索引：索引的叶节点就是数据节点。而非聚簇索引的叶节点仍然是索引节点，只不过有一个指针指向对应的数据块。
3. 聚集索引：物理存储按照索引排序；非聚集索引：物理存储不按照索引排序

#### 优化排序

1. 尽量减少额外的排序，通过索引直接返回有序数据
2. 适当加大**max_length_for_sort_data**系统变量，
3. 尽量只使用必要的字段，select具体的字段名字，而不是select *，这样可以减少排序区的使用，提高SQL性能
4. MySQL会对GROUP BY后的所有字段排序

#### 读写分离

#### 表结构优化

水平拆分、垂直拆分和逆规范化

#### 硬件升级

是用RAID10磁盘阵列，RAID10兼具RAID1的可靠性和RAID0的优良并发读写性能

#### 使用表分区

 跨多个磁盘来分散查询，能获得更大的吞吐量，需要一定的硬件条件

### 事务

1. **原子性（Atomicity）：** 事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成，要么完全不起作用；
2. **一致性（Consistency）：** 执行事务后，数据库从一个正确的状态变化到另一个正确的状态；
3. **隔离性（Isolation）：** 并发访问数据库时，一个用户的事务不被其他事务所干扰，各并发事务之间数据库是独立的；
4. **持久性（Durability）：** 一个事务被提交之后。它对数据库中数据的改变是持久的，即使数据库发生故障也不应该对其有任何影响。

### 并发事务带来哪些问题

- **脏读（Dirty read）:** 当一个事务正在访问数据并且对数据进行了修改，而这种修改还没有提交到数据库中，这时另外一个事务也访问了这个数据，然后使用了这个数据。因为这个数据是还没有提交的数据，那么另外一个事务读到的这个数据是“脏数据”，依据“脏数据”所做的操作可能是不正确的。（**读取了未提交的数据**）
- **丢失修改（Lost to modify）:** 指在一个事务读取一个数据时，另外一个事务也访问了该数据，那么在第一个事务中修改了这个数据后，第二个事务也修改了这个数据。这样第一个事务内的修改结果就被丢失，因此称为丢失修改。 例如：事务1读取某表中的数据A=20，事务2也读取A=20，事务1修改A=A-1，事务2也修改A=A-1，最终结果A=19，事务1的修改被丢失。
- **不可重复读（Unrepeatableread）:** 指在一个事务内多次读同一数据。在这个事务还没有结束时，另一个事务也访问该数据。那么，在第一个事务中的两次读数据之间，由于第二个事务的修改导致第一个事务两次读取的数据可能不太一样。这就发生了**在一个事务内两次读到的数据是不一样**的情况，因此称为不可重复读。
- **幻读（Phantom read）:** 幻读与不可重复读类似（**一个是新增、一个是修改**）。它发生在一个事务（T1）读取了几行数据，接着另一个并发事务（T2）插入了一些数据时。在随后的查询中，第一个事务（T1）就会发现多了一些原本不存在的记录，就好像发生了幻觉一样，所以称为幻读。（**在一个事务内两次读到的数据是不一样（多了）**）

###  **四个隔离级别** 

**MySQL的默认 隔离级别 就是 可重复读（Repeatable）,Oracle默认 读取已提交（Read committed）**

- **READ-UNCOMMITTED(读取未提交)：** 最低的隔离级别，允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**。

- **READ-COMMITTED(读取已提交)：** 允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**。

- **REPEATABLE-READ(可重复读)：** 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生**。

- **SERIALIZABLE(可串行化)：** 最高的隔离级别，完全服从ACID的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。

- | 隔离级别                   | 脏读 | 不可重复读 | 幻读 |
  | :------------------------- | ---- | ---------- | ---- |
  | READ-UNCOMMITTED读取未提交 | ×    | ×          | ×    |
  | READ-COMMITTED读取已提交   | √    | ×          | ×    |
  | REPEATABLE-READ可重复读    | √    | √          | ×    |
  | SERIALIZABLE可串行化       | √    | √          | √    |

###  **表级锁和行级锁** 

- **表级锁：** MySQL中锁定 **粒度最大** 的一种锁，**对当前操作的整张表加锁**，实现简单，资源消耗也比较少，加锁快，不会出现死锁。其锁定粒度最大，触发锁冲突的概率最高，并发度最低，MyISAM和 InnoDB引擎都支持表级锁。
- **行级锁：** MySQL中锁定 **粒度最小** 的一种锁，**只针对当前操作的行进行加锁**。 行级锁能大大减少数据库操作的冲突。其加锁粒度最小，并发度高，但加锁的开销也最大，加锁慢，会出现死锁。 InnoDB引擎支持行级锁。

### UNION ALL 而不是 UNION

- UNION 会把两个结果集的所有数据**放到临时表中后再进行去重**操作
- UNION ALL **不会再对结果集进行去重** 操作

### in 和 exists的区别　

使用in ,sql语句是先执行子查询，也就是先查询子表，将查询到的结果和主表做一个笛卡尔积，将结果进行筛选

使用exists是先查主表 ,再查子表

in 是把外表和内表作hash 连接，而exists是对外表作loop循环

 对于主表数据较多时，我们使用in速度比exist更快，反之，从子表较大时，使用exist插叙速度更快（都会使用索引）,

 如果使用的是not in与not exists，直接使用not exists，因为not in 会进行全表扫描不走索引，not exists会走索引。

### 分页

 使用 MyBatis 提供的插件接口(PageHelper)，实现自定义插件，在插件的拦截方法内**拦截待执行的 sql，然后重写 sql** 

**分页优化**

使用子查询优化

使用 id 限定优化

使用临时表优化

### 大数据量查询

- 普通查询，如果数据流过大会造成内存溢出，不能关闭**sqlsession**
- 游标查询，建立一个临时空间来存放需要被读取的数据，不会和DML冲突，占空间费性能
- 流式查询，MySQL Server 会**通过输出流**将 SQL 结果集返回输出，也就是 **向本地的内核对应的 Socket Buffer 中写入数据**，通过ResultHandler 接口的 handleResult 方法，可以获取到已转换后的 Java 实体类

### **binlog**

指二进制日志，它记录了数据库上的所有改变，并以二进制的形式保存在磁盘中，它可以用来查看数据库的变更历史、数据库增量备份和恢复、MySQL的复制（**主从数据库的同步**就是订阅binlog日志）。MySQL的复制是“**推**”的，而不是“拉”的，主库会启动一个Binlog dump的线程，将变更的记录从这个位置开始一条一条的发给备库。备库一直监听主库过来的变更，接收到一条，才会在本地应用这个数据变更。

binlog有三种格式：

- statement：基于SQL语句的复制，每一条会修改数据的sql都会记录在binlog中
- row：基于行的复制，它不记录sql语句上下文相关信息，仅保存哪条记录被修改(5.1.5版本的MySQL)
- mixed：混合模式复制，实际上就是Statement与Row的结合(5.1.8版本)

### redo log与undo log实现Mysql原子性，持久性

redo的组成

- 一是内存中重做日志缓冲（redo log buffer）,是易失的，在内存中
- 重做日志文件（redo log file），是持久的，保存在磁盘中

1. 先将原始数据从磁盘中读入内存中，修改数据的内存拷贝
2. 生成一条重做日志并写入redo log buffer，记录的是数据被修改后的值
3. 当事务commit时，将redo log buffer中的内容刷新到redo log file，对redo log file采用追加写的方式
4. 定期将内存中修改的数据刷新到磁盘中

undo主要记录的是数据的逻辑变化，为了在发生错误时回滚之前的操作，需要将之前的操作都记录下来，然后在发生错误时才可以回滚。

undo是一种逻辑日志，有两个作用：

- 用于事务的回滚
- **MVCC**：**多版本并发控制**，主要是为了提高数据库的并发性能，做到在发生读—写请求冲突时不用加锁，这个读是指的`快照读`，而不是`当前读`，当前读是一种加锁操作，是`悲观锁`。mvcc用来解决读—写冲突的无锁并发控制，就是为事务分配`单向增长`的`时间戳`。**为每个数据修改保存一个版本，版本与事务时间戳相关联。读操作只读取该事务开始前的数据库快照**。

undo log分为：

- insert undo log：指insert操作中产生的undo log,因为insert操作的记录，只对事务本身可见，对其他事务不可见。故该undo log可以在事务提交后直接删除，不需要进行purge操作。
- update undo log：是对delete和update操作产生的undo log，该undo log可能需要提供MVCC机制，因此不能在事务提交时就进行删除。提交时放入undo log链表，等待purge线程进行最后的删除。

#### undo log是否是redo log的逆过程

undo log是逻辑日志，对事务回滚时，只是将数据库逻辑地恢复到原来的样子。

而redo log是物理日志，记录的是数据页的物理变化，显然undo log不是redo log的逆过程。

### Mybatis

（1）Mybatis是一个半ORM（对象关系映射）框架，它内部封装了JDBC，加载驱动、创建连接、创建statement等繁杂的过程，开发者开发时只需要关注如何编写SQL语句，可以严格控制sql执行性能，灵活度高。

（2）作为一个半ORM框架，MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO映射成数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

（3）通过xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过java对象和 statement中sql的动态参数进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射为java对象并返回。（从执行sql到返回result的过程）。

（4）由于MyBatis专注于SQL本身，灵活度高，所以比较适合对性能的要求很高，或者需求变化较多的项目，如互联网项目。

#### Mybaits的优点

1、基于SQL语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响，SQL写在XML里，解除sql与程序代码的耦合，便于统一管理；提供XML标签，支持编写动态SQL语句，并可重用。

2、与JDBC相比，减少了50%以上的代码量，消除了JDBC大量冗余的代码，不需要手动开关连接；

3、很好的与各种数据库兼容（因为 MyBatis 使用 JDBC 来连接数据库，所以只要JDBC支持的数据库MyBatis都支持）。

4、能够与Spring很好的集成；

5、提供映射标签，支持对象与数据库的ORM字段关系映射；提供对象关系映射标签，支持对象关系组件维护。

#### MyBatis框架的缺点

1、SQL语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写SQL语句的功底有一定要求。

2、SQL语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。

#### 工作原理

![img](https://img-blog.csdnimg.cn/20210506164058195.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ4Nzk1NjA3,size_16,color_FFFFFF,t_70)

1. **读取MyBatis配置文件**：mybatis-config.xml为MyBatis的全局配置文件，配置了MyBatis的运行环境等信息，例如数据库连接信息。
2. 加载映射文件。映射文件即SQL映射文件，该文件中配置了操作数据库的SQL语句，需要在MyBatis配置文件mybatis-config.xml中加载。mybatis-config.xml文件可以加载多个映射文件，每个文件对应数据库中的一张表。
3. **构造会话工厂**：通过MyBatis的环境等配置信息构建会话工厂SqlSessionFactory。
4. **创建会话对象**：由会话工厂创建SqlSession对象，该对象中包含了执行SQL语句的所有方法。
5. **Executor执行器**：MyBatis底层定义了一个Executor 接口来操作数据库，它将根据SqlSession传递的参数动态地生成需要执行的SQL语句，同时负责查询缓存的维护。
6. **MappedStatement 对象**：在Executor接口的执行方法中有一个MappedStatement类型的参数，该参数是对映射信息的封装，用于存储要映射的SQL语句的id、参数等信息。
7. **输入参数映射**：输入参数类型可以是Map、List等集合类型，也可以是基本数据类型和POJO类型。输入参数映射过程类似于 JDBC对preparedStatement对象设置参数的过程。
8. **输出结果映射**：输出结果类型可以是Map、List等集合类型，也可以是基本数据类型和POJO类型。输出结果映射过程类似于 JDBC对结果集的解析过程。

#### #{}和${}

 `${}`是 Properties 文件中的**变量**占位符 ，属于静态文本替换，查询时需加引号

 `#{}`是 sql 的**参数**占位符，替换为**?**号，可以有效的防止SQL注入，提高系统安全性。

#### 分页

Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页。可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，limit

#### 延迟加载

在Mybatis配置文件中，可以配置是否启用延迟加载**lazyLoadingEnabled**=true|false。

它的原理是，使用CGLIB创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用a.getB().getName()，拦截器invoke()方法发现a.getB()是null值，那么就会单独发送事先保存好的查询关联B对象的sql，把B查询上来，然后调用a.setB(b)，于是a的对象b属性就有值了，接着完成a.getB().getName()方法的调用。这就是延迟加载的基本原理。

#### 缓存

Mybatis的一级、二级缓存:

1）一级缓存: **基于 PerpetualCache 的 HashMap 本地缓存**，其存储作用域为 **sqlSession**，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。

2）二级缓存是用来解决一级缓存**不能跨会话共享**的问题的，默认关闭，开启了二级缓存，只要sqlSession的nameSpace相同，查询的数据会存到二级缓存中，底层还是HashMap结构。

如果你的MyBatis使用了二级缓存，并且你的Mapper和select语句也配置使用了二级缓存，那么在执行select查询的时候，MyBatis会先从二级缓存中取输入，其次才是一级缓存，即MyBatis查询数据的顺序是：二级缓存  —> 一级缓存 —> 数据库。

3）对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 清空。(C/U/D：create增、delete删、update改)

#### Executor执行器

**SimpleExecutor：**每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。

**ReuseExecutor：**执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map<String, Statement>内，供下一次使用。简言之，就是重复使用Statement对象。

**BatchExecutor：**执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。与JDBC批处理相同。

作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。

#### 常用注解

insert、update、delete、select、result、resultMap、param

#### 在insert后返拿到自增主键

1. 想要获取自增主键id，应该通过对象的getId()方法，而并不是insert的返回值，insert的返回值表示的是影响行数
2. 在mapper.xml中：useGeneratedKeys="true"、keyProperty="id"，这两个属性的作用：

　　共同决定了sql执行后，会将主键封装到id属性上；

　　自增主键封装到了对象的id属性上了，那么想要获取，直接调用对象的getId()方法就可以了

## 五、JVM

### 内存区域

![img](https://img-blog.csdnimg.cn/img_convert/9e63c759aa9514c40536c7cdad53d98a.png)

#### 堆

存放对象实例，几乎所有的对象实例以及数组都在这里分配内存

Java 堆是垃圾收集器管理的主要区域

可以细分为：新生代和老年代（1:4）：再细致一点有：Eden 空间、From Survivor、To Survivor 空间，比例：8:1:1

#### 程序计数器

#### Java 虚拟机栈

会出现两种错误：StackOverFlowError 和 OutOfMemoryError

生命周期和线程相同，描述的是 Java 方法执行的内存模型

主要存放了编译期可知的各种数据类型，对象引用

-Xss 选项来设置线程的最大栈空间

#### 本地方法栈

用于存放该本地方法的**局部变量表、操作数栈、动态链接、方法返回地址**。

也会出现 StackOverFlowError 和 OutOfMemoryError 两种错误

**本地方法栈则为虚拟机使用到的 Native 方法服务**

局部变量表内容越多，栈帧越大，栈深度越小

#### 方法区

永久代

运行时常量池是方法区的一部分

#### 元空间

存放的是类的元数据，大小只由系统内存控制，可以加载更多的类

### 对象在虚拟机中创建过程

类加载检查、分配内存、初始化零值、设置对象头、执行init方法进行初始化

### 垃圾回收

#### 如何判断对象是否死亡

##### 1、引用计数法

给对象中添加一个**引用计数器**，每当有一个地方引用它，计数器就加 1；当引用失效，计数器就减 1；任何时候计数器为 0 的对象就是不可能再被使用的。(会有循环引用的问题)

##### 2、可达性分析算法

**“GC Roots”** 的对象作为起点，从这些节点开始向下搜索，节点所走过的路径称为引用链，当一个对象到 GC Roots 没有任何引用链相连的话，则证明此对象是不可用的。（不是非死不可的，先判死缓，**finalize**()方法）

###### 可以作为GC Root的对象：

1. 虚拟机栈正在引用的对象
2. 本地方法栈中正在引用的对象
3. 静态属性引用的对象
4. 方法区常量引用的对象

#### 引用类型

1、强引用：最常见，只要还有强引用指向一个对象，就不会回收

2、软引用：可有可无，内存足够不回收，内存不足时，回收

3、弱引用：发现了立即回收

4、虚引用：形同虚设，和没有任何引用一样，在任何时候都可能被垃圾回收

#### 可达性级别

1. 强可达：一个对象可以不通过引用访问到的情况
2. 软可达：只能通过软引用访问到的情况
3. 弱可达：只能通过弱引用访问的情况
4. 幻象可达：不存在其他引用，并且finalize过了，只有幻象引用指向这个对象
5. 不可达：意味着对象可以被清除了

#### Minor GC 和 Major GC

Minor GC：简单理解就是发生在年轻代的GC（Young GC）

触发条件：当Eden区满了的时候，会触发Minor GC

Major GC 是清理老年代

 S0,S1先转换再转移Eden区。

Full GC 是清理整个堆空间—包括年轻代和老年代

在进行Minor GC之前，JVM会先检查老年代最大可用连续空间是否大于新生代历次晋升到老年代对象的平均大小，如果大于，将尝试进行一次Minor GC，否则就进行Full GC（全局GC）。

老年代运用标记-整理算法回收垃圾

#### fullGc在什么时候发生 

- System.gc()方法的调用
- 老年代空间不足
- 永久区空间不足
- 堆中分配很大的对象

#### 垃圾收集算法

##### 1、标记-清除算法，有内存碎片化问题

##### 2、复制算法，有一定的浪费

##### 3、标记-整理算法

##### 4、分代收集算法，新生代(Eden，S0，S1），老年代

#### 垃圾收集器

 ![img](https://camo.githubusercontent.com/e5b0e914fca887cfb0906a3a73b30a60d8fa984b/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d31312f31316539646364306631656534663235383336653666316334373130346335312d6e65772d696d61676536396531633536612d316434302d343933612d393930312d3665666336343761303166332e706e67) 

<img src="https://p3-tt.byteimg.com/origin/pgc-image/98a4cb3656a14624bae029e7fc3112a2?from=pc" alt="《我想进大厂》之JVM夺命连环10问" style="zoom:67%;" />

stop-the-world停止用户线程所有工作进行垃圾回收

##### Serial 收 集器

串行收集器，新生代采用复制算法，老年代采用标记-整理算法

![ Serial 收集器 ](https://snailclimb.gitee.io/javaguide/docs/java/jvm/pictures/jvm%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6/46873026.png)

##### ParNew 收集器

新生代采用复制算法，老年代采用标记-整理算法

##### Parallel Scavenge 收集器(默认)

新生代采用复制算法，老年代采用标记-整理算法

可设置垃圾回收线程数，最大停顿时间，吞吐量

##### Serial Old 收集器

##### Parallel Old 收集器

##### CMS 收集器

专用老年代，基于标记-清除算法，尽量减少停顿时间

存在内存碎片问题，长时间运行会发生full GC

占用CPU资源，和用户线程争抢

![CMS 垃圾收集器 ](https://snailclimb.gitee.io/javaguide/docs/java/jvm/pictures/jvm%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6/CMS%E6%94%B6%E9%9B%86%E5%99%A8.png)

##### G1 收集器

Jdk1.9默认选型，面向服务器的垃圾收集器,主要针对配备多颗处理器及大容量内存的机器. 以极高概率满足 GC 停顿时间要求的同时,还具备高吞吐量性能特征

- **初始标记**
- **并发标记**
- **最终标记**
- **筛选回收**

##### Jdk默认回收器：

- jdk1.7 默认垃圾收集器Parallel Scavenge（新生代【标记-复制算法】）+Parallel Old（老年代【标记整理算法】）
- jdk1.8 默认垃圾收集器Parallel Scavenge（新生代）+Parallel Old（老年代）
- jdk1.9 默认垃圾收集器G1【从局部(两个Region之间)来看是基于"标记—复制"算法实现，从整体来看是基于"标记-整理"算法实现】

#### 堆外内存的回收机制

概念：JVM启动时分配的内存，称为堆内存，与之相对的，把内存对象分配在Java虚拟机的堆以外的内存就是堆外内存，但是这部分的内存并不归JVM管理，GC算法并不会对它们进行回收，所以在使用堆外内存时，要格外小心，防止内存一直得不到释放，造成线上故障。

申请：JDK的ByteBuffer类提供了一个接口allocateDirect(int capacity)进行堆外内存的申请，底层通过unsafe.allocateMemory(size)实现

回收：JDK中使用**DirectByteBuffer**对象来表示堆外内存，每个DirectByteBuffer对象在初始化时，都会创建一个对应的Cleaner对象，这个Cleaner对象会在合适的时候执行unsafe.freeMemory(address)，从而回收这块堆外内存。

![《我想进大厂》之JVM夺命连环10问](https://p1-tt.byteimg.com/origin/pgc-image/08358c9369e64b979844717f41f46e57?from=pc)

Java对象保存在内存中时，由以下三部分组成：

1，对象头：**Mark Word**记录和描述对象的部分，记录了对象和锁有关的信息、**指向类的指针**主要是存储元数据的地址、**数组数据部分**，专门用来存储数组数据。

2，实例数据：对象的实例数据就是在java代码中能看到的属性和他们的值

3，对齐填充字节

### 类加载过程

 ![img](https://camo.githubusercontent.com/68465e752e28fd5e7c6a6d442c19f05305c8f043/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d31312f2545372542312542422545352538412541302545382542442542442545382542462538372545372541382538422d2545352541452538432545352539362538342e706e67) 

### 类加载器

JVM 中内置了三个重要的 ClassLoader，除了 BootstrapClassLoader 其他类加载器均由 Java 实现且全部继承自`java.lang.ClassLoader`：

1. **BootstrapClassLoader(启动类加载器)** ：最顶层的加载类，由C++实现，负责加载 `%JAVA_HOME%/lib`目录下的jar包和类或者或被 `-Xbootclasspath`参数指定的路径中的所有类。
2. **ExtensionClassLoader(扩展类加载器)** ：主要负责加载目录 `%JRE_HOME%/lib/ext` 目录下的jar包和类，或被 `java.ext.dirs` 系统变量所指定的路径下的jar包。
3. **AppClassLoader(应用程序类加载器)** :面向我们用户的加载器，负责加载当前应用classpath下的所有jar包和类。

#### 双亲委派模型

 类加载的时候，系统会首先判断当前类是否被加载过。已经被加载的类会直接返回，否则才会尝试加载。加载的时候，首先会把该请求委派该父类加载器的 `loadClass()` 处理，因此所有的请求最终都应该传送到顶层的启动类加载器 `BootstrapClassLoader` 中。当父类加载器无法处理时，才由自己来处理。**优点：保证Java代码稳定运行**

 <img src="https://camo.githubusercontent.com/4311721b0968c1b9fd63bdc0acf11d7358a52ff6/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f636c6173736c6f616465725f5750532545352539422542452545372538392538372e706e67" alt="img" style="zoom:67%;" /> 

### JVM调优

调优目标：提供响应时间，提高吞吐量，无需过多调优，JVM在不断优化

开启打印GC日志，方便排查问题

**设置合理的堆内存大小**，减少GC次数和耗时，更加稳定

**选择合适的垃圾回收器**

设置合理的垃圾回收器的参数

禁止系统System.gc()，防止手动误触发FGC造成问题

1. 为了打印日志方便排查问题最好开启GC日志，开启GC日志对性能影响微乎其微，但是能帮助我们快速排查定位问题。-XX:+PrintGCTimeStamps -XX:+PrintGCDetails -Xloggc:gc.log
2. 一般设置-Xms=-Xmx，这样可以获得固定大小的堆内存，减少GC的次数和耗时，可以使得堆相对稳定
3. -XX:+HeapDumpOnOutOfMemoryError让JVM在发生内存溢出的时候自动生成内存快照，方便排查问题
4. -Xmn设置新生代的大小，太小会增加YGC，太大会减小老年代大小，一般设置为整个堆的1/4到1/3
5. 设置-XX:+DisableExplicitGC禁止系统System.gc()，防止手动误触发FGC造成问题

### 服务器优化性能

性能瓶颈：网络IO、磁盘IO、CPU

CPU：并发编程、少用锁、减少系统调用、减少遍历、优化架构

网络IO：使用epoll代替select、使用非阻塞模式开发

磁盘IO：使用缓存cache、利用顺序写

寻找瓶颈：top命令、free命令、vmstat性能分析工具

### 服务器挂了怎么办

1. 查找top检查服务器负载是否有问题

2. 在服务器中查看网站的访问记录：这些访问记录存储在：/home/对应的网站名/access-logs/对应的网站名

   可以先通过tail查看，查看出异常的ip的时候可以通过grep进行过滤查看，在这个文件一般都可以找到恶意爬虫、恶意访问的记录，这些往往有可能是导致mysql数据库挂掉的原因。

3. 这个时候先对数据库进行重启，再对apache进行重启，找出恶意访问的ip把它禁止掉

4. 查找数据库错误日志

### OOM原因

**1. 堆内存溢出**

　java.lang.OutOfMemoryError: Java heap space：这种是java堆内存不够，一个原因是真不够分配，另一个原因是程序中有死循环； 
　　如果是java堆内存不够的话，可以通过调整JVM下面的配置来解决： 
　　< jvm-arg>-Xms3062m < / jvm-arg> 
　　< jvm-arg>-Xmx3062m < / jvm-arg> 

一般的排查方式可以通过设置 -XX: +HeapDumpOnOutOfMemoryError 在发生异常时dump出当前的内存转储快照来分析

**2. 方法区（运行时常量池）和元空间溢出**

方法区和堆一样，是线程共享的区域，包含 class 文件信息、运行时常量池、常量池。运行时常量池和常量池的主要区别是具备动态性，也就是不一定非要是在 class 文件中的常量池中的内容才能进入运行时常量池，运行期间也可以可以将新的常量放入池中，比如 String 的 intern 方法。

intern 本身是一个 native 方法，它的作用是：如果字符串常量池中已经包含一个等于此 String 对象的字符串，则返回代表池中这个字符串的 String 对象；否则，将此 String 对象包含的字符串添加到常量池中，并且返回 String 对象的引用。

**3. 直接内存溢出**

比如在 NIO 中可以使用 native 函数直接分配堆外内存就容易导致 OOM 的问题。

**4. 栈内存溢出**

1. 如果线程请求的栈深度大于虚拟机所允许的最大深度(递归深度过长导致)，将抛出 StackOverflowError 异常。
2. 如果虚拟机栈可以动态扩展，并且扩展时无法申请到足够的内存，抛出 OutOfMemoryError 异常。

**5、代码错误**

### JDK命令行工具

这些命令在 JDK 安装目录下的 bin 目录下：

- jps (JVM Process Status）: 显示当前所有的Java进程pid的命令

- jstat（ JVM Statistics Monitoring Tool）: **监视Java虚拟机的统计信息，可以显示GC的信息**

- jinfo (Configuration Info for Java) : 显示虚拟机配置信息;

  jinfo -flag pid查看进程配置信息

- jmap (Memory Map for Java) :生成**堆**转储快照，是一个可以输出所有内存中对象的工具；会触发full gc，生产环境不使用

- jhat (JVM Heap Dump Browser ) : 用于分析 堆heapdump 文件，它会建立一个 HTTP/HTML 服务器，让用户可以在浏览器上查看分析结果;

  jstat -gc -h10 pid 1000 每隔1秒打印JVM内存情况

- jstack (Stack Trace for Java):生成虚拟机当前时刻的线程快照，线程快照就是当前虚拟机内每一条线程正在执行的方法堆栈的集合。

### JVM可视化工具

Jconsole

JvisualVM

GCViewwer

### GC 调优策略

 将新对象预留在新生代 

 大对象进入老年代 

 合理设置进入老年代对象的年龄 

 设置稳定的堆大小 ， 堆大小设置有两个参数：`-Xms` 初始化堆大小，`-Xmx` 最大堆大小。 

一般不需要进行GC优化

### JVM的分代年龄为什么是15

对象的分代年龄占4位，也就是0000，最大值为1111也就是最大为15

### Tomcat调优

| 配置项                                           | 默认            | 建议 | 注意         |
| ------------------------------------------------ | --------------- | ---- | ------------ |
| ConnectionTimeout超时时间                        | 20S             | 减少 |              |
| maxThreads处理连接最大线程数                     | 200             | 增加 | 不是越大越好 |
| acceptCount(backlog)等待接受accept的请求数量限制 | 100             | 增加 | socket参数   |
| maxConnections最大连接处理数                     | nio 1W apr 8192 | 不变 |              |

总连接数 = acceptCount + connections

- connections：Tomcat能接受的请求限制

- acceptCount：超过Tomcat能接受的请求数后，堆积在操作系统的数量

调整connections

connections小于maxThread的时候，需要调大，大20%，多余的会堆积到Tomcat的work处理线程池中

调整acceptCount

可调整为   最大并发数 - connections，实际上不需要调整。

调整处理线程数

理想线程数 = （1 + 代码阻塞时间 / 代码执行时间）*  CPU数量

理想CPU占用率：80-90%

#### 加载指定的包

修改catalina.sh文件 

找到start条件语句的位置【elif [ "$1" = "start" ] ; then】，在执行java命令的后面增加指定jar目录的参数-Djava.ext.dirs

## 六、容器

### 1:Docker

容器化技术，Go语言开发，用于创建和使用Linux容器

借助Docker，可将容器当做轻巧、模块化的虚拟机使用，可以高效地创建、部署和复制容器

![在这里插入图片描述](https://img-blog.csdnimg.cn/8eea79f6e00446de8fd9e8f774c3bf9f.png#pic_center)

### 2:kubernetes

是一种可自动实施Linux容器操作的开源平台，可以帮助用户省去容器化过程的许多手动部署和扩展操作。

借助K8s编排功能，可以构建跨多个容器的应用服务、跨集群调度、扩展这些容器，并长期持续管理这些容器的健康状况。



## 七、网络知识

#### 三次握手

三次握手的目的是建立可靠的通信信道，说到通讯，简单来说就是数据的发送与接收，而三次握手最主要的目的就是双方确认自己与对方的发送与接收是正常的。**发送方发送SYN信号，接收方返回SYN/ACK信号，发送方再返回ACK信号。**

<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019/7/%E4%B8%89%E6%AC%A1%E6%8F%A1%E6%89%8B2.png" alt="TCP三次握手" style="zoom:67%;" />

四次挥手

断开一个 TCP 连接则需要“四次挥手”：

- 客户端-发送一个 FIN，用来关闭客户端到服务器的数据传送
- 服务器-收到这个 FIN，它发回一 个 ACK，确认序号为收到的序号加1 。和 SYN 一样，一个 FIN 将占用一个序号
- 服务器-关闭与客户端的连接，发送一个FIN给客户端
- 客户端-发回 ACK 报文确认，并将确认序号设置为收到序号加1

<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019/7/TCP%E5%9B%9B%E6%AC%A1%E6%8C%A5%E6%89%8B.png" alt="TCP四次挥手" style="zoom:67%;" />

#### 网络体系结构

OSI七层模型

应用层-表示层-会话层-运输层-网络层-数据链路层-物理层

TCP/IP

应用层-运输层-网际层-网络接口层

![五层体系结构](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019/7/%E4%BA%94%E5%B1%82%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84.png)

打开一个网页，整个过程会使用哪些协议

<img src="https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-11/url%E8%BE%93%E5%85%A5%E5%88%B0%E5%B1%95%E7%A4%BA%E5%87%BA%E6%9D%A5%E7%9A%84%E8%BF%87%E7%A8%8B.jpg" alt="img" style="zoom: 50%;" />

#### HTTP 和 HTTPS 的区别

1. **端口** ：HTTP的URL由“http://”起始且默认使用端口80，而HTTPS的URL由“https://”起始且默认使用端口443。

2. 安全性和资源消耗：

   HTTP协议运行在TCP之上，所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份。HTTPS是运行在**SSL/TLS**之上的HTTP协议，SSL/TLS 运行在TCP之上。所有传输的内容都经过**加密**，加密采用对称加密，但对称加密的密钥用服务器方的证书进行了非对称加密。所以说，HTTP 安全性没有 HTTPS高，但是 HTTPS 比HTTP耗费更多服务器资源。

   - 对称加密：密钥只有一个，加密解密为同一个密码，且加解密速度快，典型的对称加密算法有DES、AES等；
   - 非对称加密：密钥成对出现（且根据公钥无法推知私钥，根据私钥也无法推知公钥），加密解密使用不同密钥（公钥加密需要私钥解密，私钥加密需要公钥解密），相对对称加密速度较慢，典型的非对称加密算法有RSA、DSA等。

http协议状态码：

2开头：成功

3开头：这类状态码代表需要客户端采取进一步的操作才能完成请求。重定向

4开头：请求错误

5开头：服务器错误

#### TCP 协议如何保证可靠传输

1. 应用数据被分割成 TCP 认为最适合发送的数据块。
2. TCP 给发送的每一个包进行编号，接收方对数据包进行排序，把有序数据传送给应用层。
3. **校验和：** TCP 将保持它首部和数据的检验和。这是一个端到端的检验和，目的是检测数据在传输过程中的任何变化。如果收到段的检验和有差错，TCP 将丢弃这个报文段和不确认收到此报文段。
4. TCP 的接收端会丢弃重复的数据。
5. **流量控制：** TCP 连接的每一方都有固定大小的缓冲空间，TCP的接收端只允许发送端发送接收端缓冲区能接纳的数据。当接收方来不及处理发送方的数据，能提示发送方降低发送的速率，防止包丢失。TCP 使用的流量控制协议是可变大小的滑动窗口协议。 （TCP 利用滑动窗口实现流量控制）
6. **拥塞控制：** 当网络拥塞时，减少数据的发送。
7. **ARQ协议：** 也是为了实现可靠传输的，它的基本原理就是每发完一个分组就停止发送，等待对方确认。在收到确认后再发下一个分组。
8. **超时重传：** 当 TCP 发出一个段后，它启动一个定时器，等待目的端确认收到这个报文段。如果不能及时收到一个确认，将重发这个报文段。

#### 安全控制

spring中添加监听器、拦截器filter，单点登陆(SSO)，cookie+session，token，数据加密，网关有安全控制功能

cookie：存储登录信息，保存在浏览器端(客户端)，关闭时效，不安全

session：会话，存储在服务端：通过cookie存储一个session_id，服务器端压力大，集群模式下，服务器不共享session

token：令牌，token与session的不同主要在登陆认证成功后，会对当前用户数据进行加密，生成一个加密字符串token，返还给客户端（服务器端并不进行保存），浏览器会将接收到的token值存储在Local Storage中，服务器对浏览器传来的token值进行解密，解密完成后进行用户数据的查询，如果查询成功，则通过认证，实现状态保持。基于token认证机制的应用**不需要去考虑用户在哪一台服务器登录**了，这就为应用的扩展提供了便利，解决了session扩展性的弊端

##### 越权解决策略

基于角色的权限控制

1. 首先用户登录时，通过Shiro框架，将用户信息放入Subject中，并将该用户对用的项目id和权限id放入redis中。
2. 再分析并整理对应相关越权的接口，将这些接口整理，并且添加拦截器，将这些接口进行拦截。
3. 拦截之后，从Shiro框架的Subject获取用户信息，根据用户信息查询该用户对应的项目id或活动id。
4. 因为有些接口对项目操作，有的接口只对活动操作，有的接口对这两个都操作，所以我选择先判读项目id是否为空，然后再判读项目id存不存在在redis中，不存在直接返回false，若存在，再判断活动id的情况。

#### 加密技术

对称加密、非对称加密

DES：对称算法，数据加密标准，速度较快，适用于加密大量数据的场合；

RSA：由 RSA 公司发明，是一个支持变[密钥的公共密钥算法，需要加密的文件块的长度也是可变的，非对称算法

MD5：严格来说不算加密算法，只能说是摘要算法；

对MD5算法简要的叙述可以为：MD5以512位分组来处理输入的信息，且每一分组又被划分为16个32位子分组，经过了一系列的处理后，算法的输出由四个32位分组组成，将这四个32位分组级联后将生成一个128位散列值。

## 八、linux操作

### 1、故障排查

**CPU问题**：业务逻辑问题（死循环）、频繁GC、上下文切换过多

可以使用jstack来分析

先用ps找到对应进程，top看哪个占用比较高，再拿nid用找到对应的堆栈信息，jstack pid|grep 'nid' -C5 -color，再分析

jstat -gc pid 1000对GC分析观察

**频繁fullGC**使用jstat -gcutil或者查看gc.log日志，查看内存回收情况

vmstat查看上下文切换

**磁盘问题**

df -hl查看文件系统状态

iostatiostat -d -k -x 分析磁盘问题

iotop 定位文件读写来源

lsof -p pid确定具体文件读写情况

**内存问题**：OOM、GC、堆外内存

内存问题大多都是堆外内存，OOM、Stack Overflow

pmap查看进程占用内存情况

**GC问题**

**网络问题**：网络连接、端口占用、超时

netstat

telnet

## 九、面试技巧

面对HR或者其他Level比较低的面试官时

1. 能不能谈谈你**作为一个公司老员工对公司的感受**? (这个问题比较容易回答，不会让面试官陷入无话可说的尴尬境地。另外，从面试官的回答中你可以加深对这个公司的了解，让你更加清楚这个公司到底是不是你想的那样或者说你是否能适应这个公司的文化。除此之外，这样的问题在某种程度上还可以拉进你与面试官的距离。)
2. 能不能问一下，你当时因为什么原因选择加入这家公司的呢或者说这家公司有哪些地方吸引你？有什么地方你觉得还不太好或者可以继续完善吗？ （类似第一个问题，都是问面试官个人对于公司的看法。），**这个公司吸引你的地方**
3. 我觉得我这次表现的不是太好，你有什么建议或者评价给我吗？(这个是我常问的。我觉得说自己表现不好只是这个语境需要这样来说，这样可以显的你比较谦虚好学上进。)
4. 接下来我会有一段空档期，有什么值得注意或者建议学习的吗？ （体现出你对工作比较上心，自助学习意识比较强。）
5. 这个岗位为什么还在招人？ (岗位真实性和价值咨询)
6. 大概什么时候能给我回复呢？ (终面的时候，如果面试官没有说的话，可以问一下)
7. 前后端分离吗
8. 是微服务架构吗
9. 上班时间
10. 开发团队是多少人
11. 业务方向

面对部门领导

1. 部门的主要人员分配以及对应的主要工作能简单介绍一下吗？
2. 未来如果我要加入这个团队，你对我的期望是什么？ （部门领导一般情况下是你的直属上级了，你以后和他打交道的机会应该是最多的。你问这个问题，会让他感觉你是一个对他的部门比较上心，比较有团体意识，并且愿意倾听的候选人。）
3. 公司对新入职的员工的培养机制是什么样的呢？ （正规的公司一般都有培养机制，提前问一下是对你自己的负责也会显的你比较上心）
4. 以您来看，这个岗位未来在公司内部的发展如何？ (在我看来，问这个问题也是对你自己的负责吧，谁不想发展前景更好的岗位呢？)
5. 团队现在面临的最大挑战是什么？ (这样的问题不会暴露你对公司的不了解，并且也能让你对未来工作的挑战或困难有一个提前的预期。)

面对Level比较高的(比如总裁,老板)

1. 贵公司的发展目标和方向是什么？ （看下公司的发展是否满足自己的期望）
2. 与同行业的竞争者相比，贵公司的核心竞争优势在什么地方？ （充分了解自己的优势和劣势）
3. 公司现在面临的最大挑战是什么？
