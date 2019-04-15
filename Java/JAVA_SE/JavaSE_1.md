# <center>JAVA_SE(第一部分)<center>  
##  ❤1、Java基础  
### 1、为什么重写equals还要重写hashcode  
&emsp;&emsp;对Object来说，判断集合中是否已经存在该对象，先调用该对象hashCode方法，查看二者hashcode是否相同，若不同则equals直接返回false，否则再调用equals方法。【目的：当向集合中插入对象时，判别在集合中是否已经存在该对象时能够**提高效率**】  
###  2、说一下map的分类和常见的情况  
​       Map主要用于存储健值对，根据键得到值，因此不允许键重复（若重复则覆盖），但允许值重复。  
![](http://java-picture.oss-cn-hangzhou.aliyuncs.com/javaSE/map.png)
**HashMap:**  
&emsp;&emsp;Hashmap 是一个最常用的Map，它根据键的HashCode值存储数据，根据键可以直接获取它的值，具有很快的访问速度。  
​       遍历时，取得数据的顺序是完全随机的。  
​       HashMap最多只允许一条记录的键为Null；允许多条记录的值为 Null。  
​       HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap，可能会导致数据的不一致。如果需要同步，可以用 Collections的synchronizedMap方法使HashMap具有同步能力，或者使用ConcurrentHashMap。  
**Hashtable:**  
&emsp;&emsp;Hashtable与 HashMap类似，它继承自Dictionary类，不同的是:  
<li> 它不允许记录的键或者值为空。   
<li> 它支持线程的同步，即任一时刻只有一个线程能写Hashtable，因此也导致了 Hashtable在写入时会比较慢。  
**LinkedHashMap:**  
&emsp;&emsp;LinkedHashMap 保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的。在遍历的时候会比HashMap慢，不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比LinkedHashMap慢，因为LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和容量有关。  
**TreeMap:**  
&emsp;&emsp;TreeMap实现SortMap接口，能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。

### 3、Object若不重写hashCode()的话，hashCode()如何计算出来的？
&emsp;&emsp;通过相应的hash函数（哈希算法）进行计算

### 4、==比较的是什么？
&emsp;&emsp;比较的是对象的内存地址。

### 5、若对一个类不重写，它的equals()方法是如何比较的？

1.   先判断内存地址是否相同  如果内存地址相同 那么字符串就是相同的 返回true
2.   先判断当前字符串和参数字是否属于同一类
3.   比较字符串长度（也就是char[]数组）是否相等  不相等返回false
4.   逐个字符比较
### 6、java8新特性
**Lambda 表达式**  
&emsp;&emsp;Lambda允许把函数作为一个方法的参数（函数作为参数传递进方法中）。  
**方法引用:**  
&emsp;&emsp;方法引用提供了非常有用的语法，可以直接引用已有Java类或对象（实例）的方法或构造器。与lambda联合使用，方法引用可以使语言的构造更紧凑简洁，减少冗余代码。  
**默认方法:**  
&emsp;&emsp;默认方法就是一个在接口里面有了一个实现的方法。  
**新工具:**  
&emsp;&emsp;新的编译工具，如：Nashorn引擎 jjs、 类依赖分析器jdeps。  
**Stream API:**  
&emsp;&emsp;新添加的Stream API（java.util.stream） 把真正的函数式编程风格引入到Java中。  
**Date Time API:**  
&emsp;&emsp;加强对日期与时间的处理。  
**Optional 类:**  
&emsp;&emsp;Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常。  
**Nashorn, JavaScript 引擎:**  
&emsp;&emsp;Java 8提供了一个新的Nashorn javascript引擎，它允许我们在JVM上运行特定的javascript应用。
### 7、说说Lamda表达式的优缺点。
**优点：**  
1.   简洁、非常容易并行计算。  
2.   可能代表未来的编程趋势。  
3.   结合 hashmap 的 computeIfAbsent 方法，递归运算非常快。java有针对递归的专门优化。  

**缺点：**  
1. 若不用并行计算，很多时候计算速度没有比传统的 for 循环快。（并行计算有时需要预热才显示出效率优势，并行计算目前对 Collection 类型支持的好，对其他类型支持的一般）  
2. 不容易调试。  
3. 代码不容易让其他语言的程序员看懂。  
### 8、一个十进制的数在内存中是怎么存的？
&emsp;&emsp;以二进制补码的形式存储，其中，正数的补码仍为其原码，负数则原码按位取反再加一。
### 9、为啥有时会出现4.0-3.6=0.40000001这种现象？
&emsp;&emsp;二进制小数难以精确表达十进制小数，计算机在计算十进制小数的运算过程中需要先转换为二进制再运算，再该过程中，很容易出现差错。
### 10、Java支持的数据类型有哪些？什么是自动拆装箱？
**基本数据类型：**   
&emsp;&emsp;byte（1字节），short（2字节），int（4字节），long（8字节），char（2字节），boolean（不确定，取值是true/false），float（4字节），double（8字节）  
**引用数据类型：**  
&emsp;&emsp;包括数组，集合，字符串，接口以及类等  
**自动装箱/自动拆箱:**  
&emsp;&emsp;就是指基本数据类型可以和其对应包装类之间自动转换，如Integer 和 int 可以自动转换； Float和float可以自动转换。如果一个基本类型值出现在需要对象的环境中，会自动装箱，需要数值进行运算会自动开箱。
### 11、什么是值传递和引用传递？ 
**值传递：**是对于基本数据类型的变量而言的。传递的是该变量的一个副本，改变副本并不影响原变量  
**引用传递：**是对于对象型变量而言的。传递的是该变量地址的一个副本，并不是该对象本身
### 12、数组(Array)和列表(ArrayList)有什么区别？什么时候应该使用Array而不是ArrayList？
<li>Array可以包含基本类型和对象类型，ArrayList只能包含对象类型。
<li>Array大小是固定的，ArrayList的大小是动态变化的。
<li>ArrayList提供了更多的方法和特性，比如：addAll()，removeAll()，iterator()等等。
<li>对于基本类型数据，集合使用自动装箱来减少编码工作量。但是，当处理固定大小的基本数据类型的时候，这种方式相对比较慢。 
 
### 13、你了解大O符号(big-O notation)么？你能给出不同数据结构的例子么？
&emsp;&emsp;时间复杂度。

### 14、String是最基本的数据类型吗?
&emsp;&emsp;不是，String是引用数据类型。

### 15、int 和 Integer 有什么区别
1、Integer是int的包装类，int则是java的一种基本数据类型   
2、Integer变量必须实例化后才能使用，而int变量不需要   
3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值   
4、Integer的默认值是null，int的默认值是0

### 16、String 和StringBuffer的区别
**1）String:**是对象不是原始类型.为不可变对象,一旦被创建,就不能修改它的值.对于已经存在的String对象的修改都是重新创建一个新的对象,然后把新的值保存进去.String 是final类,即不能被继承  
**2）StringBuffer:**是一个可变对象,当对他进行修改的时候不会像String那样重新建立对象。它只能通过构造函数来建立对象被建立以后,在内存中就会分配内存空间,并初始保存一个null.向StringBuffer中付值的时候可以通过它的append方法.
### 17、我们在web应用开发过程中经常遇到输出某种编码的字符，如iso8859-1等，如何输出一个某种编码的字符串？
	 	tempStr = new String(str.getBytes("ISO-8859-1"), "GBK");//把"ISO-8859-1"转化为“GBK”编码
    	tempStr = tempStr.trim(); 		//trim()用于去掉字符串两端多余的空格


### 18、&和&&的区别？
<li>Java中&&和&都是表示逻辑与运算符，都表示逻辑运输符and，当两边的表达式都为true的时候，整个运算结果才为true，否则为false。  
<li>&&的短路功能：当第一个表达式的值为false的时候，则不再计算第二个表达式；&则两个表达式都执行。  
<li>&可以用作位运算符，当&两边的表达式不是Boolean类型的时候，&表示按位操作。
### 19、在Java中，如何跳出当前的多重嵌套循环？
&emsp;&emsp;标号，用break+标号跳出；break跳出；注入异常跳出。

### 20、你能比较一下Java和JavaSciprt吗？
<li>Java和JavaScript最重要的区别是一个是静态语言，一个是动态语言。  
<li>目前的编程语言的发展趋势是函数式语言和动态语言。在Java中类（class）是一等公民，而JavaScript中函数（function）是一等公民。
<li>java在运行前必须经过编译，而javaScript则不需要。

### 21、简述正则表达式及其用途。
&emsp;&emsp;在编写处理字符串的程序时，经常会有查找符合某些复杂规则的字符串的需要。正则表达式就是用于描述这些规则的工具。换句话说，正则表达式就是记录文本规则的代码。

### 22、Java中是如何支持正则表达式操作的？
&emsp;&emsp;Java中的String类提供了支持正则表达式操作的方法，包括：matches()、replaceAll()、replaceFirst()、split()。此外，Java中可以用Pattern类表示正则表达式对象，它提供了丰富的API进行各种正则表达式操作，请参考下面的代码。

		String str = "北京市(朝阳区)(西城区)(海淀区)";
		Pattern p = Pattern.compile(".*?(?=\\()");
		Matcher m = p.matcher(str);