1、9种基本数据类型的大小，以及他们的封装类？

  基本类型	封装类型		大小（字节）
  int 		Integer		4
  short     Short		2
  long 		Long		8
  byte		Byte		1
  char		Character	2
  boolean 	Boolean
  float		Float		4
  double	Double		8
  
2、Switch能否用String做参数？

在jdk 7 之前，switch 只能支持 byte、short、char、int 这几个基本数据类型和其对应的封装类型。switch后面的括号里面只能放int类型的值，但由于byte，short，char类型，它们会 自动 转换为int类型（精精度小的向大的转化），所以它们也支持。

注意，对于精度比int大的类型，比如long、float，doulble，不会自动转换为int，如果想使用，就必须强转为int，如(int)float;

jdk1.7后，整形，枚举类型，boolean，字符串都可以.
其实，jdk1.7并没有新的指令来处理switch string，而是通过调用switch中string.hashCode,将string转换为int从而进行判断。

3、equals和==的区别

==操作符专门用来比较两个变量的值是否相等，也就是用于比较变量所对应的内存中所存储的数值是否相同，要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作符。

equals方法是用于比较两个独立对象的内容是否相同，就好比去比较两个人的长相是否相同，它比较的两个对象是独立的。

==比较两个人是否究竟是真正同一个人，equals一般用来比较两个人在逻辑上是否相等（比如规定两人成年之后身高相同就算两人相同等等），想怎么定义就怎么定义，如果不覆盖equals方法的话，默认仍然是比较两人是否同一个人（废话，两个人都还处于胚胎状态，都没有具体特征，怎么可能在逻辑上比较）

4、Object有哪些公用方法?

wait()、notify()、notifyAll()、equals（）、hashCode()、toString()  :  对象的字符串表达形式

5、java的四种引用，强弱软虚,以及用到的场景

强引用的一定不会被清理.
JVM保证抛出out of memory之前，清理所有的软引用对象.

强引用（StrongReference）:宁可报oom，虚拟机也不会回收该类对象。
软引用（SoftReference）:在内存即将不够用的时候，会回收该类对象。软引用可用来实现内存敏感的高速缓存。
弱引用（WeakReference）:在虚拟机gc的时候，会回收该类对象。这个类通常用于在某处保存对象引用，而又不干扰该对象被GC回收，通常用于Debug、内存监视工具等程序中。
虚引用（PhantomReference）：就是形同虚设，与其他几种引用都不同，虚引用并不会决定对象的生命周期。如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。
虚引用主要用来跟踪对象被垃圾回收器回收的活动。虚引用与软引用和弱引用的一个区别在于：虚引用必须和引用队列 （ReferenceQueue）联合使用。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之 关联的引用队列中。

6、HashCode的作用

hashCode 方法返回该对象的哈希码值。
hashCode的存在主要是提高查找的快捷性。

hashCode是用于查找使用的，而equals是用于比较俩个对象是否相等的。
在HashMap HashSet中,hashCode()是判断放进容器里的两个对象是否相等的依据。如果自己写容器，那就修改覆写改方法

7、ArrayList、LinkedList、Vector的区别

ArrayList类似于C中的数组，插入复杂，查找方便
LinkedList类似于C中的链表，插入简单，查找复杂度较高
Vector类似于ArrayList,但是在java 1.5以后就不推荐使用了。Vecotr是同步的。

8、String、StringBuffer、StringBuilder的区别

三者在执行速度方便的比较：StringBuilder > StringBuffer  > String

字符串常亮 String : 操作少量数据
字符串变量 StringBuffer （线程安全）: 多线程操作字符串缓冲区 下操作大量数据
字符串变量 StringBuilder （非线程安全）: 单线程操作字符串缓冲区 下操作大量数据

9、Map 、 Set 、List 、 Queue 、Stack 的特点与用法

map   :根据key找value
set   :无序，元素不能重复
list  :类似数据，有序，可以重复元素
queue :队列，先进先出
stack :栈，先进后出

10、HashMap和HashTable的区别

HashMap是非线程安全的，只是用于单线程环境下，多线程下可以采用concurrent并发包下的concurrentHashMap。
HashMap实现了Serializable接口，因此支持序列化，实现了Cloneable接口，能被克隆。
HashMap内部实现是一个默认16大小的数组和单链表实现的，当发生hash碰撞的时候用链表来解决，支持自动扩容，默认加载因子是0.75。

HashTable是线程安全的，可以用于多线程。同样实现了Serializable，支持序列化，实现了cloneable接口，能被克隆。

HashTable中，key和value都不允许出现null值。但是如果在HashTable中有类似的put(null,null)的操作，同样可以编译通过，因为key和value都是Object类型，但运行时会抛出nullPointerException异常，这是Jdk的规范规定的。

HashMap中，null可以作为键，这样的键只有一个；可以有一个活多个键所对应的值为null。当get()方法返回null值时，可能是HashMop中没有该键，也可能是该键所对应的值为null。因此，在HashMap中不能用get()方法判断HashMap中是否存在某个键，而应该用containsKey()方法来判断。

内部实现使用的数组初始化和扩容方式不同
HashTable在不指定容量的情况下，默认容量为11	，而HashMap为16，HashTable不要求底层数组的容量一定要为2的整数次幂，而Hashmap则要求一定要为2的整数次幂。
HashTable扩容时，将容量变为原来的2倍+1，而HashMap扩容时，将容量变为原来的2倍。

11、HashMap和ConcurrentHashMap的区别，HashMap的底层源码。
有并发的时候用ConcurrentHashMap，效率比用锁的HashMap好。
HashMap底层源码用（Entry）数组 + 链表的形式实现。

12、TreeMap、HashMap、LinkedHashMap的区别。
LinkedHashMap也是一个HashMap，但是内部维护了一个双向链表，可以保持顺序。
TreeMap 可以用于排序（根据键排序，默认是升序）。HashSet是通过HashMap实现的，TreeSet是通过TreeMap实现的，只不过Set用的是map的key，Map的key和Set都有一个共同的特性就是集合的唯一性，TreeMap更是多了一种排序功能。

一般情况下，我们用的最多的是HashMap，HashMap里面存入的键值对在取出的时候是随机的，他根据键的HashCode值存储数据，根据键可以获取到他的值，具有很快的访问速度，在Map中插入、删除和定位元素，HashMap是最好的选择。
TreeMap取出来是排序好的键值对。但如果您要按自然顺序或自定义顺序遍历键，那么TreeMap会更好。
LinkedHashMap是HashMap的一个子类，如果需要输出和输入的顺序相同，那么用LinkedHashMap可以实现。

13、Collection包结构，与Collections的区别。

Collection     List --- ArrayList,LinkedList,Vector 
				Set --- HashSet,TreeSet
				Map --- HashMap,TreeMap,HashTable
			
Collection是集合类的上级接口，子接口主要有Set、List、Map
Collections是针对集合类的一个帮助类，提供了操作集合的方法：一系列静态方法实现对集合的搜索、排序、线程安全化等操作。

14、try catch finally , try里有return，finall还执行吗？

必须执行。  如果try里有return,finally也有return,会执行finall中的return.

15、Exception 与 Error包结构。OOM你遇到过哪些结构，SOF你遇到过哪些情况

1：java异常结构： 
2：Thorwable类所有异常和错误的超类，有两个子类Error和Exception，分别表示错误和异常。其中异常类Exception又分为运行时异常(RuntimeException)和非运行时异常，这两种异常有很大的区别，也称之为不检查异常（Unchecked Exception）和检查异常（Checked Exception）。 
3：运行时异常也就是在代码中不用try块或者throws捕获或者抛出异常，而是由系统在运行时出现时自动抛出，如果在代码中用try块捕获，会出现一个问题就是抛异常的时候不会打印，也就是不会显示出来，对于查找有一定困难。 
4：Error一般是程序无法处理的错误，如OutofMemoryError，StackOverFlowError，ThreadDeath错误等。这类一般java虚拟机直接选择线程终止。Exception异常中运行时异常包括NullPointerException，IndexOutOfBoundsException等，其他的异常则为检查异常，如IoException，SqlException或者自己写的异常。 
5：OOM（outOfMemoryError）（统一将Error也叫异常，因为他是异常体系的一部分），如果往一个List列表里面不断的加入对象，则最终会出现OOM异常主要是针对java堆的。 
6：Sof（stackOverflowError）对于栈溢出这种情况，我们可以通过设置-Xss参数来控制每一线程栈的大小，当减小每个线程栈大小，同时在函数方法内存放比较大或者多的局部变量，就会发生栈溢出。当然sof只放生在虚拟机栈和本地方法栈，不会发生在java堆和方法区中。如果要在方法区发生sof，可以设置MaxPermSize参数，然后调用String.inter（）方法不断的往方法区中加入字符串。 
7：java运行时常量池和普通常量池区别：如果在编译时的常量，则存放入普通常量池，当运行时时如采用String.intern（）动态加入的常量或者从远端调用产生的常量，则存入运行时常量池中。当然，运行时常量池和静态常量池都是属于方法区的一部分，受maxpermsize参数的影响。 

16、java 面向对象的三个特征与含义

封装 ：就是将一个实物抽象化为一个类，然后通过一个类去创建一个对象。
继承 ：也就是对父类方法的继承，包括对接口的实现也属于继承。易于扩展，降低耦合。
多态 ：当子类对象的引用赋给父类引用的时候就会发生多态（简单说就是向上转型，向上转型是多态机制的一种表现形式）多态的实现依赖于多态机制，及动态绑定：也就是在编译的时候编译器只通过父类引用只知道调用方法的签名，无法知道调用哪一个方法体，要确定这个调用的方法体，只有通过new创建一个对象以后，并将该方法对应的栈帧加入虚拟机栈中才能直达实际的方法体，也就是方法体的后期绑定，因此就不能像使用final修饰方法一样，编译器自己可以优化方法。Final修饰的方法不可覆盖，也就关闭了动态绑定。由此可知覆盖和重载都是多态的一种表现形式。

17、Override和Overload的含义及区别

Override是覆盖，覆盖是子类和父类多态性的表现形式。
Overload是重载，重载的原则是方法的签名不同，方法签名不包括返回值，重载是一个类中多态的表现形式。

18、interface于abstract类的区别

interface是接口，可以有常量，所有的方法默认都是public，而且不能实现。
abstract类 比其他普通类多了个抽象方法，而且是必须有抽象方法。

使用理念上区分：
1、并不是所有的类都是用来描绘对象的，如果一个类中没有足够的信息来描绘一个具体的对象，这样的类就是抽象类。
2、要想使继承关系合理，父类和派生类之间必须存在“is a”关系，即父类和派生类在概念本质上应该是相同的，因此抽象类要满足这种情况。对于Interface来说则不然，并不要求interface的实现者和interface定义在概念本质上是一致的，仅仅实现了interface的契约而已。interface表示的是“like a”关系。

19、static class 与 non static class 的区别

1、内部静态类不需要有指向外部类的引用，但非静态内部类需要持有对外部类的引用。
2、非静态内部类可以访问外部类的静态和非静态成员，静态类不能访问外部类的非静态从成员，他只能访问外部类的静态成员。

20、java多态的实现原理

java中实例方法才有多态的，在运行时动态绑定，类的成员变量实在编译时就决定了。

21、实现线程的俩种方法：继承Thread和实现Runable

22、线程同步的方法：synchronized、lock、reenrantLock等

23、锁的等级：方法锁、对象锁、类锁
对象锁是用于对象实例方法，或者一个对象实例上的。
类锁是用于类的静态方法或者一个类的class对象上的，我们知道，类的对象实例可以有很多个，但是每个类只有一个class对象，所以不同的对象实例的对象锁是互补干扰的，但是每个类只有一个类锁。

24、ThreadLocal的设计理念与作用

java中的ThreadLocal类允许我们创建只能被同一个线程读写的变量。
因此，如果一段代码含有一个ThreadLocal变量的引用，及时俩个线程同时执行这段代码，他们也无法访问到对方的ThreadLocal变量。虽然所有的线程都能访问到这个ThreadLocal实例，但是每个线程却只能访问到自己通过调用ThreadLocal的set()方法设置的值。及时是俩个不同线程在同一个ThreadLocal对象上设置的不同的值，他们仍然无法访问到对象的值。内部实现用同步Map。
private Map values = Collections.synchronizedMap(new HashMap());

25、ThreadPool用法与优势。

在多线程环境中使用Thread Pool,可以提高运行效率，不用每次新建一个线程，循环利用线程。

26、wait()和sleep()的区别。


