
Collection->
list 称为线性表，用于存储有先后次序的一组元素。元素可以重复储存，每个元素有下标序号。
set

List接口常见实现类有两个：{ArrayList;LinkedList }
ArrayList 与LinkedList 的区别：ArrayList：利用可变长度数组实现的线性表；LinkedList：采用双向循环链表实现的线性表
ArrayList 与数组的关系：1.ArryList内部封装了一个对象数组在添加元素时候，如果数组容量不够会自动扩容。
2.ArrayList 内部就是数组，但是其提供了操作方法，所以用起来毕数组更加方便
ArrayList适合尾部追加,避免尾部和中部修改。LinkedList 适合头尾部修改，避免中部修改。

数组实现的线性表 
1.任何位置读取都迅速
2.修改、插入时候，由于异步修改会引起数据大规模移动，其性能会不太好。但是尾部修改或插入不会发生数据移动，性能不错。
使用建议：读取多修改少时候使用

LinkedList：双向循环链表
1.头尾读取性能好，中部读取性能差。因为中部读取的时候需要逐一遍历元素，造成性能差。
2.修改、插入时候，头尾快，中间慢。
使用建议：头尾读取修改多，中部、读取少时候选用
建议：由于大多数情况下数据经常是读取多，修改少如果没有明确使用倾向时候选择ArrayList

java.util.Map接口---查找表
Map是一个非常常用的数据结构，体现的样子为一个多行两列的表格。其中左列称为key，右列称为value。Map右一个要求，就是key不允许重复的常用实现类：java.util.HasMap，又名散列表，哈希表HashMap是当今查询速度最快的数据结构！

Java反射机制：可以在程序运行期间多态获取一个类的消息，从而做到在运行期觉得实例化某个类，获取其定义的方法和属性并且进行调用利用反射机制可以提高代码的灵活性，但是不能过度的依赖反射机制。
类对象：Class。类对象的每个实例用于表示JVM加载的一个类每个被JVM加载的类都有且只有一个类对象的实例与之对应提供类对象可以获取其表示的类的一系列信息： 获取类名字，类定义的构造方法，属性，方法超类等等信息。反射是基于类对象进行的。
获取一个类的类对象方式主要有： 1：每个类都有一个静态属性class，可以用于	获取该类的类对象。比如： String.class,int.class。2：使用Class的静态方法forName，指定要加载的类的完全限定名（包名。类名），记载并获取该类的类对象3：使用类加载器ClassLoader加载指定的类。


parameterType非select
useGeneratedKeys="true" insert


1.基于数组实现，是一个动态数组，其容量能自动增长。
2.ArrayList不是线程安全的，建议在单线程中使用，多线程可以选择Vector或CopyOnWriteArrayList。
3.实现了RandomAccess接口，可以通过下标序号进行快速访问。
4.实现了Cloneable接口，能被克隆。
5.实现了Serializable接口，支持序列化。

HashMap是不安全的；HashTable线程安全的（使用了synchronized关键字来保证线程安全）
HashMap中key和value可以为空；HashTable中value不可以为空

哈希值的使用不同，HashTable直接使用对象的hashCode，代码是这样的：      
  int hash = key.hashCode();       int index = (hash & 0x7FFFFFFF) % tab.length; 
而HashMap重新计算hash值，而且用与代替求模： 
  int hash = hash(k); int i = indexFor(hash, table.length);
