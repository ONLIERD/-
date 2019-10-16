# AbstractCollection #
## 介绍 ##
	public abstract class AbstractCollection<E> implements Collection<E>
- AbstractCollection是一个抽象类,实现了Collection接口,是Collection接口的概括性的实现
- 保留的Collection接口的两个抽象方法:

		public abstract Iterator<E> iterator();
    	public abstract int size();
-  若想自定义一个不可变集合,只需要继承该类且实现iterator()和size()两个抽象方法
-  若想自定义一个可变集合,必须重写add()方法,并且iterator()方法返回的迭代器必须实现其remove()方法
- 自定义集合时,应该提供无参和集合的构造方法
## 字段属性 ##
    private static final int MAX_ARRAY_SIZE = Integer.MAX_VALUE - 8;
- 集合的最大长度,Integer类型4字节即32位(bit),所以其最大长度为2的31次方-1=2147483639
## 构造方法 ##
### protected AbstractCollection() ###
- 无参构造方法,空实现调用父类的构造方法

## 抽象方法 ##
### public abstract Iterator<E> iterator() ###
- 保留的Collection的迭代器方法,供开发者自定义集合时实现
### public abstract int size() ###
- 保留的Collection的集合长度方法,供开发者自定义集合时实现

## 实例方法 ##
### public boolean isEmpty() ###
		return size() == 0;
- 用集合长度来判断是否为空,所以抽象方法size()需要实现

### public boolean contains(Object o) ###
        Iterator<E> it = iterator();
        if (o==null) {
            while (it.hasNext())
                if (it.next()==null)
                    return true;
        } else {
            while (it.hasNext())
                if (o.equals(it.next()))
                    return true;
        }
        return false;
- 通过其迭代器方法遍历集合来判断集合是否包含指定元素,所以抽象方法iterator()需要实现
- 可以传入null值,因为集合中可能存在null值,此时也计入包含

### public Object[] toArray() ###
        Object[] r = new Object[size()];
        Iterator<E> it = iterator();
        for (int i = 0; i < r.length; i++) {
            if (! it.hasNext()) // fewer elements than expected
                return Arrays.copyOf(r, i);
            r[i] = it.next();
        }
        return it.hasNext() ? finishToArray(r, it) : r;
- 先声明一个与集合等大的对象数组,用迭代器遍历集合,依次赋值到对象数组中,当遍历到集合的最后一个元素时,用Arrays.copyof()方法将对象数组复制到新的T[]数组并返回










