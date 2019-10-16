#  Collection 集合  #
## 基本介绍  ##
- Collection&lt;E&gt;是集合的顶层接口,继承了可迭代接口Iterable&lt;E&gt;
- Collection的常用的一个抽象类和两个子接口:  
	AbstractCollection&lt;E&gt;  
	List&lt;E&gt;----允许有重复的元素  
	Set&lt;E&gt;-----不允许有重复的元素
## 方法 ##
### 1.int Size() ###
- 返回元素集合数量,若大于Integer.MAX_VALUE,则返回Integer.MAX_VALUE
### 2. boolean isEmpty() ###
- 集合是否包含元素
### 3. boolean contains(Object o) ###
- 集合是否包含指定的元素
- 判断条件:当且仅当集合中至少包含一个满足(o == null? e == null : o.equals(e))的元素e时返回true。
- 可以重写E的equals方法，来指定在何种情况下两个E对象是equals相等的。
### 4. Iterator<E> iterator() ###
- 返回基于集合元素的迭代器,但不保证元素返回的顺序,除非该集合类的实例提供了顺序保证
### 5.Object[] toArray()  ###
- 返回一个包含所有集合元素的数组
- 返回的数组是安全的,因为该集合不维护数组的引用,即该方法一定会分配新数组,即使原集合由数组支持
- 返回类型是Object[],且无法被强制转换,只能在遍历时进行单个元素的强制转换
### 6.T[] toArray(T[] a) ###
- 返回一个包含所有集合元素的数组
- 返回的数组的运行时类型是指定数组的类型
- Java5引入泛型之后,相比于Object[] toArray(),使用toArray(T[] a)编译器会帮助进行强制转换和元素检测
- 集合大小如果小于指定数组大小,则会分配一个与集合等大的新数组来容纳元素并返回  
  集合大小如果大于指定数组大小,则会用指定数组容纳集合元素,并将后一个数组内容设为null,其余则保持不变  
  指定数组可以不为空

		list:1,2,3
    	array:a,b,c,d,e
		list.toArray(array);
		结果:1,2,3,null,e
- 上诉操作可以用转化后的数组来确定原集合长度,如果原集合无null值
- 若集合保证了迭代器返回元素的顺序,那返回的数组也要保持顺序一致
### 7.boolean add(E e) ###
- 为集合添加元素
- 支持该操作的集合可能会对add的元素进行限制,如类型限制,拒绝add空值等
- 如果因调用导致集合更改,则返回true  
  如果该集合不允许重复且已经包含指定元素,则返回false,该情况这可能发生在Set集合中,List集合只会返回true  
### boolean remove(Object o) ###
- 删除指定集合元素
- 当该方法调用的结果是一个元素被删除(或者说存在指定元素),则返回true  
  元素不存在,则返回false  
  存在多个相同元素时,删除其中一个,返回true
###  boolean containsAll(Collection<?> c) ###
- 该集合是否包含指定集合的所有元素,重复元素不影响返回值
### boolean addAll(Collection<? extends E> c) ###
- 添加指定集合的所有元素到该集合
- 调用后集合发生改变则返回true
- 如果在操作正在进行时修改了指定的集合，则此操作的行为是未定义的。这意味着如果指定的集合是此集合，并且此集合是非空的，则此调用的行为是未定义的。
### boolean removeAll(Collection<?> c) ###
- 删除该集合内存在的指定集合的所有元素
### default boolean removeIf(Predicate<? super E> filter) ###
- 删除所有满足给定条件的集合元素
- 该方法会通过集合的迭代器进行迭代判断,并调用集合的迭代器的remove方法进行删除,如果该集合的迭代器不支持remove,则抛出UnsupportedOperationException
- Since 1.8+
### boolean retainAll(Collection<?> c) ###
- 删除该集合除指定集合内元素的所有元素
### void clear() ###
- 清空集合
### boolean equals(Object o) ###
### int hashCode() ###
### default Spliterator<E> spliterator() ###
    return Spliterators.spliterator(this, 0);
- 在该集合中的元素上创建一个可分割迭代器
- TODO
- 可分割迭代器参见《iterator迭代器》
- since 1.8
### default Stream<E> stream() ###
    return StreamSupport.stream(spliterator(), false);
- 返回以此集合为数据源的序列化的串行流
- 当spliterator()方法不能返回一个不可变、并发或延迟绑定的可分割迭代器时，该方法应该被重写
- since 1.8
### default Stream<E> parallelStream()
	return StreamSupport.stream(spliterator(), true);
- 以此集合为其源返回一个可能并行的流,允许返回序列流
- 当spliterator()方法不能返回一个不可变、并发或延迟绑定的可分割迭代器时，该方法应该被重写
- since 1.8
