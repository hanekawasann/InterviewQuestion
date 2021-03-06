[TOC]

## 基本概念

**JDK和JRE的区别**

JDK是java的开发工具包，里面包含了各种类库和工具。JRE是java程序的运行环境

**finally代码块和finalize()方法的区别**

- 无论是否抛出异常，finally代码块都会执行，它主要是用来释放应用占用的资源。
- finalize()方法是Object类的一个protected方法，它是在对象被垃圾回收之前由Java虚拟机来调用的。

**`&&`和`&`的区别，`||`和`|`的区别**

- & -> 与，| -> 或
- &&和||是逻辑运算符，&和|是按位运算符。
- &&当两侧都为真输出真，||当两侧中有一侧为真输出真。
- &当两侧都为1是输出1，|当两侧中有一侧为1输出1。

**==跟equals()的区别**

==：如果作用于基本数据类型变量，则直接比较其存储的 “值”是否相等。如果作用于引用类型变量，则比较的是指向的对象的地址。

equals：不能作用于基本数据类型，默认比较指向的对象的地址。

**序列化与反序列化**

序列化是将对象的状态信息转换为可以存储或传输的形式的过程。

反序列化是与序列化相分的过程。

序列化作用：
- 以某种存储形式使自定义对象持久化。
- 将对象从一个地方传递到另一个地方。
- 使程序更具维护性。
> 维护性？

## 面向对象

**面向对象的特征**

- 封装：隐藏内部实现，只暴露公共行为
- 继承：提高代码可重用性和可扩展性
- 多态：体现现实生活中相似对象的差异性
- 抽象：抽取现实世界中相似对象的共同点

**类的实例化顺序**

1. 父类静态成员变量
1. 父类静态代码块
1. 父类非静态代码块
1. 子类静态成员变量
1. 子类静态代码块
1. 子类非静态代码块
1. 父类实例成员变量
1. 父类构造函数
1. 子类实例成员变量
1. 子类构造函数

**抽象类和接口的区别**

- 抽象类和接口都不能直接实例化，都能声明抽象方法，但是接口只能声明抽象方法，JDK8中，接口可以声明静态方法和默认方法。
- 接口只能声明静态成员变量，而抽象类可以声明实例成员变量。
- 接口不能声明非静态代码块，而抽象类可以。

**类可以继承多个类么，接口可以继承多个接口么，类可以实现多个接口么**

类只能单继承，接口可继承接口，并可多继承接口。

**继承和聚合的区别**

- 继承表示is-a
- 聚合表示has-a

**隐式类型转换和显示类型转换**

- 隐式类型转换是指类型从小到大，子类转化为父类，JVM自动完成。
- 显式类型转换是指类型从大到小，父类转化为子类，可能存在精度损失，需要显式编码。
> 即向上转型和向下转型？

**类方法和实例方法**

- 类方法是静态方法，与类关联，不需要创建类的实例。
- 实例方法是非静态方法，与类的实例关联。

**重载与重写**

- 重载（Overload ）是在一个类里面，名字相同、而参数不同、返回类型可以相同也可以不同的方法。
- 重写（Override）是子类对父类的允许访问的方法的实现过程进行重新编写。

**构造方法能否被重写**

构造方法不能被重写，可以被重载

**访问权限**

- 权限关键字：private、默认、protected、public
- 修饰对象：类、方法
- 修饰范围：类内部、同包类、子类、任意类

**堆和栈有什么不同**

- 栈内存存储的是局部变量，而堆内存存储的是实体
- 栈内存的更新速度要快于堆内存，因为局部变量的生命周期很短
- 栈内存存放的变量生命周期一旦结束就会被释放，而堆内存存放的实体会被垃圾回收机制不定时的回收

## API

### 常用类

**基本数据类型有哪些？对应的包装类是什么？什么是自动拆装箱？什么时候自动装箱不起作用？**

- byte、short、int、long、float、double、char、boolean
- Byte、Short、Integer、Long、Float、Double、Character、Boolean
- 基本数据类型和它对应的封装类型之间可以相互转换，从基本数据类型到封装类型叫做装箱，从封装类型到基本数据类型叫拆箱，自动拆装箱是jdk5.0提供的新特特性。
- 当我们要调用的方法中存在重载的时候，即基本类型数据作为唯一参数的方法与该基本类型包装类作为唯一参数的方法重载，这时候自动装箱不起作用。

**String能被继承吗？**

不可以，String类有final修饰符，而final不能被继承的，实现细节不允许改变。

**String对象的intern()**

intern()方法会首先从常量池中查找是否存在该常量值，如果常量池中不存在则现在常量池中创建，如果已经存在则直接返回。

**String，StringBuffer，StringBuilder的区别**

- String是字符串常量，创建之后即不能更改，是不可变对象。
- StringBuffer和StringBuilde都是字符串变量，继承和实现同一个接口（CharSequence）和类（AbstractStringBuilder），使用方法基本一致。
- StringBuffer是jdk1.0引入、线程安全，绝大多数方法都进行了synchronized同步处理。其toString方法会进行对象缓存，以减少元素的复制开销。
- StringBuilder是jdk1.5引入、非线程安全。比StringBuffer效率高。其toString方法会直接返回一个新String对象。

### 集合

**List、Set和Map的区别**

- List、Set都继承自Collection。
- List有序可重复。
- Set无序不可重复。
- Map无序不可重复，保存键值对。
> 这里的无序是指插入的顺序与插入后的顺序相比而言。

**Iterator和ListIterator的区别**

- ListIterator支持添加（add）、修改（set）、删除对象，而Iterator只支持删除对象。
- ListIterator支持向后遍历（hasNext、next）和向前遍历（hasPrevious、previous），而Iterator只支持向后遍历。
- ListIterator可以定位当前的索引位置（nextIndex、previousIndex），而Iterator不支持。

**Vector和ArrayList的区别**

同步容器（线程安全） -> 效率。

**ArrayList和LinkedList的区别**

- 它们都实现了List接口。
- ArrayList是基于索引的数据接口，底层是数组，所以查找元素很快。
- LinkedList是基于元素列表的数据接口，底层是链表，所以添加和删除元素很快。
- LinkedList比ArrayList更占内存，因为LinkedList为每一个节点存储了两个引用，一个指向前一个元素，一个指向下一个元素。

**CopyOnWriteArrayList**

CopyOnWriteArrayList是一个并发容器，而不是同步容器。每次调用add方法都会创建一个新的object数组，此数组的大小为当前数组大小加1，将之前数组中的内容复制到新的数组中，并将新增加的对象放入数组末尾，最后做引用切换将新创建的数组对象赋值给全局的数组对象。

**HashSet和TreeSet的区别**

- HashSet基于哈希表实现，是无序的；TreeSet基于二叉树实现，支持排序，默认升序排序。
- HashSet允许放入一个null，TreeSet不允许放入null。
- 它们都是不重复的集合，HashSet依靠hashCode和equals区分重复数据，而TreeSet依靠Comparable来区分重复数据。

**用过哪些Map类，都有什么区别**

- HashMap、LinkedHashMap、TreeMap、ConcurrentHashMap。
- HashMap采用哈希表来存储的，底层通过数组+链表+红黑树（JDK1.8增加了红黑树部分）。
- LinkedHashMap按照插入顺序排序。
- TreeMap默认按照升序排序。
- ConcurrentHashMap是并发容器，JDK1.8放弃了分段锁，改为CAS算法（处理器架构支持的比较并交换指令）、非阻塞算法。
> 红黑树是一种自平衡二叉查找树。

**如果HashMap的大小超过了负载因子定义的容量**

- 加载因子是表示Hsah表中元素的填满的程度。加载因子越大，填满的元素越多，空间利用率越高，冲突的机会越大，导致查找成本越高。反之，加载因子越小，填满的元素越少，空间利用率越低，冲突的机会越小，导致查找成本越小。
- 当哈希表中的条目数超出了加载因子与当前容量的乘积时，则要对该哈希表进行rehash操作（即重建内部数据结构），从而哈希表将具有大约两倍的桶数。

**HashMap和Hashtable的区别**

null值，线程安全性，速度
> 问过

**权衡是使用无序的数组还是有序的数组**

- 有序数组最大的好处在于查找的时间复杂度是O(log n)，而无序数组是O(n)。
- 有序数组的缺点是插入操作的时间复杂度是O(n)，因为值大的元素需要往后移动来给新元素腾位置。
- 相反，无序数组的插入时间复杂度是常量O(1)。

### IO

**利用FileInputStream从流中获取数据**

```java
// 读取一个字节
public int read() throws IOException;
// 读取字节数组
public int read(byte b[]) throws IOException;
public int read(byte b[], int off, int len) throws IOException;
```

### 反射

**反射是什么**

反射机制指的是程序在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法。

**Class.forName()方法的作用**

通过.class二进制文件对指定的类执行加载、连接、初始化操作，其结果是会在方法区中为该类生成一个class对象作为访问类型信息的入口，还会为类的类变量分配空间并赋值。
> 类变量即静态成员变量

## 并发

**什么是线程安全**

当多个线程访问某个类时，不管运行时环境采用何种调度方式或者这些线程将如何交替执行，并且在主调代码中不需要任何额外的同步或者协同，这个类都能表现出正确的行为，那么就称这个类是线程安全的。
> Java并发编程实战

**进程和线程的区别**

- 进程和线程的主要差别在于它们是不同的操作系统资源管理方式，进程是资源的分配和调度的一个独立单元，而线程是CPU调度的基本单元。
- 进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。
- 线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间。
- 一个程序至少有一个进程，一个进程至少有一个线程。
> 问过

**线程间通信方式**

- 内置锁、volatile、显示锁、条件队列
- 原子变量、阻塞队列

**创建线程有几种不同的方式？哪一种更好？**

- 继承Thread类、实现Runnable接口、应用程序可以使用Executor框架来创建线程池。
- Java不支持多继承，所以实现Runnable接口更加灵活。线程池也是非常高效的，很容易实现和使用。

**线程的状态**

共六种状态：
- NEW： 新建状态，线程对象已经创建，但尚未启动。
- RUNNABLE：就绪状态，可运行状态，调用了线程的start方法，已经在java虚拟机中执行，等待获取操作系统资源如CPU，操作系统调度运行。
- BLOCKED：堵塞状态。线程等待锁的状态，等待获取锁进入同步块/方法或调用wait后重新进入需要竞争锁。
- WAITING：等待状态。等待另一个线程以执行特定的操作。 Object.wait()，Thread.join()，LockSupport.park()。
- TIMED_WAITING：线程等待一段时间。调用带参数的Thread.sleep，objct.wait，Thread.join，LockSupport.parkNanos，LockSupport.parkUntil。
- TERMINATED：进程结束状态。

**线程的BLOCKED状态和WAITING状态的区别**

- BLOCKED是阻塞，线程等待锁的状态。
- WAITING是等待，该状态下等待唤醒之后进入BLOCKED。
> 问过

**sleep()和wait()的区别**

- 它们分别来自于Thread类和Obejct类。
- sleep表示休眠，当前线程释放CPU控制权，但不释放锁，在指定时间后自动醒来。
- wait表示等待，当前线程释放CPU控制权，也释放锁，通过参数可以设置直到其他线程唤醒该线程之前都不会醒来。
> 条件队列一定锁在一起使用，所以肯定会获得锁

**如何确保N个线程可以访问N个资源同时又不导致线程死锁？**

锁顺序死锁：两个线程试图以不同的顺序来获得相同的锁，导致了死锁。如果所有线程以固定的顺序来获得锁，那么在程序中就不会出现锁顺序死锁问题。
> Java并发编程实战

**悲观锁与乐观锁**

- 悲观锁：总是假设最坏情况，每次去拿数据的时候都认为别人会修改，每次在拿数据的时候都会上锁。（独占锁：内置锁、显示锁）
- 乐观锁：总是假设最好情况，每次去拿数据的时候都认为别人不会修改，不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据。这种方法需要借助冲突检查机制来判断在更新过程中是否存在来自其他线程的干扰，如果存在，这个操作将失败，并且可以重试。（原子变量类）

## 其他

**对称加密算法、非对称加密算法和散列算法**

- 对称加密算法：双方使用的同一个密钥，既可以加密又可以解密，这种加密方法称为对称加密，也称为单密钥加密。常用的有DES、AES。
- 非对称加密算法：一对密钥由公钥和私钥组成（可以使用很多对密钥）。私钥解密公钥加密数据，公钥解密私钥加密数据（私钥公钥可以互相加密解密）。常用的有RSA、ECC。
- 散列算法：单向算法，不可逆。常用的有MD5、SHA。
- 对称加密算法比非对称加密算法快，但非对称加密算法更加安全。

**Java中垃圾回收有什么目的？什么时候进行垃圾回收？**

- 回收堆内存中不再使用的对象，释放资源。
- 当对象永久地失去引用后，系统会在合适的时候回收它所占的内存。

**处理内存溢出**

内存逸出原因：加载数据过大、引用对象未清空、死循环、启动参数内存值设定过小。
- 第一步，修改JVM启动参数，直接增加内存。
- 第二步，检查错误日志，查看“OutOfMemory”错误前是否有其它异常或错误。
- 第三步，对代码进行走查和分析，找出可能发生内存溢出的位置。
