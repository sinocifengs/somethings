# <center>JAVA_SE(第二部分)<center>
## ❤2、关键字

### 1、介绍一下Syncronized锁，如果用这个关键字修饰一个静态方法，锁住了什么？如果修饰成员方法，锁住了什么？
在synchronized里面，包含有三种常见的锁状态：

- 对于普通的同步方法：   锁是当前的对象 
- 对于静态函数的同步方法：   锁是指引用当前类的class对象 
- 对于同步方法块的内容：   锁是指Synchonized括号里配置的对象
Syncronized可以修饰于代码块，实例方法，静态方法。作用是为修饰的方法加锁，提供线程安全。
### 2、介绍一下volatile？
&emsp;&emsp;volatile原意为“不稳定的、反复无常的”。其作为java中的关键词之一，用来声明变量的值可能会随着其他线程修改，使用volatile修饰的变量会强制将修改的值立即写入主存。而非volatile变量值会被放入缓存，当线程A更新了该值，线程B未必会读取到线程A更新后的值。
### 3、锁有了解嘛，说一下Synchronized和lock

| Tables        | Lock           |Synchronized  |
| :-------------: |:-------------:| :-----:|
| 内涵     | lock为接口，是显示锁（即加锁和解锁的过程可见并且需要我们自己控制） | Synchronized是关键字，是隐式锁 |
| 修饰      | Lock需要它的一些实现类来做到加锁和解锁。比如ReentrantLock。      |   Synchronized可以用来修饰方法代码块 |
| 用法| 通常需要使用try，catch，finally这种形式在finally中去unlock释放锁     |    Synchronized不需要关注锁释放，因为代码块执行完毕或者报错都会释放锁 |
| 读写锁 | Lock可以让读共享      |    S在读写锁方面没有Lock灵活，面对多个线程读取文件只能依此加锁解锁。 |

### 4、讲一讲Java里面的final关键字怎么用的？
final关键字可以用来修饰类、方法和变量（包括成员变量和局部变量）

- 当用final修饰一个类时，表明这个类不能被继承。
- 当用final修饰一个方法时，表明这个方法不能被覆盖。
- 当用final修饰一个变量时，表明这个变量为常量，且只能被赋值一次，赋值后值不再改变。
## ❤3、面向对象
### 1、wait方法底层原理
&emsp;&emsp;sleep()方法属于Thread类，而wait()方法属于Object类。sleep()方法导致了程序暂停执行指定的时间，让出cpu该其他线程，但是他的监控状态依然保持者，当指定的时间到了又会自动恢复运行状态。在调用sleep()方法的过程中，线程不会释放对象锁。而当调用wait()方法的时候，线程会放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象调用notify()方法后本线程才进入对象锁定池准备获取对象锁进入运行状态。
### 2、Java有哪些特性，举个多态的例子。
Java特性有：封装,继承,多态。举例多态: 父类引用指向子类对象，例如：
 
		Animal animal = new Dog();

### 3、String为啥不可变？
&emsp;&emsp;String为一个引用，指向其value，即字符数组对象，String是对字符数组的封装，其value为final的，当其值确定下来后，则无法进行改变。
### 4、类和对象的区别。
&emsp;&emsp;对象是对客观事物的抽象，类是对对象的抽象。类是一种抽象的数据类型。对象是类的实例，类是对象的模板。对象是通过new className产生的，用来调用类的方法;类的构造方法 
### 5、请列举你所知道的Object类的方法。
Object类有12个成员方法，按照用途可以分为以下几种 ：

**a.类的构造函数**  
**b用来判断对象是否相同的hashCode和equale函数：**equale()用于确认两个对象是否相同。hashCode()用于获取对象的哈希值，这个值的作用是检索  
**c.关于锁中的wait(),wait(long),wait(long,int),notify(),notifyAll() ：**

这几个函数体现的是Java的多线程机制  
<li> 在使用的时候要求在synchronize语句中使用
<li> wait()用于让当前线程失去操作权限，当前线程进入等待序列
<li> notify()用于随机通知一个持有对象的锁的线程获取操作权限
<li> notifyAll()用于通知所有持有对象的锁的线程获取操作权限
<li> wait(long) 和wait(long,int)用于设定下一次获取锁的距离当前释放锁的时间间隔  
**d.toString()和getClass：**toString()返回一个String对象，用来标识自己 ，getClass()返回一个Class对象  
**e.clone() ：**另存一个当前存在的对象。  
**f.用于垃圾回收的finalize()：**在进行垃圾回收时会用到，匿名对象回收之前会调用到  

### 6、重载和重写的区别？相同参数不同返回值能重载吗？
**重载：**同一个类中的多个方法具有相同的名字,但这些方法具有不同的参数列表,即参数的数量或参数类型不能完全相同。不能根据返回值类型作为重载函数的区分。  
**重写：**存在子父类之间,子类定义的方法与父类中的方法具有相同的方法名字,相同的参数表和相同的返回类型 

### 7、”static”关键字是什么意思？Java中是否可以覆盖(override)一个private或者是static的方法（都不可）？
&emsp;&emsp;static关键字表示静态的意思，用于修饰成员变量和成员函数。表示可以在没有类的实例的情况下，用类名.变量名或者类名.函数名，进行访问  
&emsp;&emsp;覆盖（重写），是子类继承父类，而父类中private修饰的方法，不能被继承，所以也不存在重写（覆盖）  
&emsp;&emsp;static修饰的方法，是静态方法，在编译时已和类名进行了绑定。而重写发生在运行时，动态绑定的。

### 8、String能继承吗？
&emsp;&emsp;不可以，String类有final修饰符，决定了其不可以被继承。

### 9、StringBuffer和StringBuilder有什么区别，底层实现上呢？
&emsp;&emsp;StringBuffer 与 StringBuilder 中的方法和功能完全是等价的。StringBuffer 中的方法大都采用了 synchronized 关键字进行修饰，因此是线程安全的；    
&emsp;&emsp;StringBuilder 没有这个修饰，可以被认为是线程不安全的。 
&emsp;&emsp;在单线程程序下，StringBuilder效率更快，因为它不需要加锁，不具备多线程安全;而StringBuffer则每次都需要判断锁，效率相对更低.

### 10、类加载机制，双亲委派模型，好处是什么？
**类加载：**JVM第一次使用到某个类时需要对这个类的信息进行加载。一个类只会加载一次，之后这个类的信息放在堆空间，静态属性放在方法区。JVM类加载器从上到下一共分为三类：  

<li>启动类加载器(Bootstrap ClassLoader)：负责加载 JAVA_HOME\lib 目录中的，或通过-Xbootclasspath参数指定路径中的，且被虚拟机认可（按文件名识别，如rt.jar）的类。
<li>扩展类加载器(Extension ClassLoader)：负责加载 JAVA_HOME\lib\ext 目录中的，或通过java.ext.dirs系统变量指定路径中的类库。
<li>应用程序类加载器(Application ClassLoader)：负责加载用户路径（classpath）上的类库。 

&emsp;&emsp;JVM通过双亲委派模型进行类的加载启动类加载器(Bootstrap ClassLoader)：负责加载 JAVA_HOME\lib 目录中的，或通过-Xbootclasspath参数指定路径中的，且被虚拟机认可（按文件名识别，如rt.jar）的类。 扩展类加载器(Extension ClassLoader)：负责加载 JAVA_HOME\lib\ext 目录中的，或通过java.ext.dirs系统变量指定路径中的类库。 应用程序类加载器(Application ClassLoader)：负责加载用户路径（classpath）上的类库。  
&emsp;&emsp;采用双亲委派的一个好处是比如加载位于rt.jar包中的类java.lang.Object，不管是哪个加载器加载这个类，最终都是委托给顶层的启动类加载器进行加载，这样就保证了使用不同的类加载器最终得到的都是同样一个Object对象。