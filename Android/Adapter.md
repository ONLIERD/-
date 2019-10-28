1. GridView/ListView是在什么时候设置对Adapter的数据监听的？
- 在setAdapter(ListAdapter adapter)中，会先取消View中原来的mAdapter中的数据监听（mAdapter.unregisterDataSetObserver(mDataSetObserver);），然后再设置对新设置的adapter的数据监听。

2. getView(int position, View convertView, ViewGroup parent)是怎么被利用的?
-  在GridView/ListView的源码中没有发现getView方法的调用，他们的父类AbsListView的obtainView中调用了getView，而obtainView又会在GridView/ListView的onMeasure和makeAndAddView中用到。

3. getCount()
- 返回底层数据的数据总个数。在ListView中，在onMeasure以及触控分发响应等过程中都会用到Adapter的getCount()函数。

4. getItem(int position)
- getItem()在AbsListView的父类AdapterView的 getSelectedItem()中被调用，然后供用户调用：从这两个函数的描述我们可以看出，我们应该在Adapter的getItem()方法中返回position对应的数据，但是不是说一定要返回用于在Item的View上展示的数据，这个还是看需求，虽然可能大部分情况都是返回View中展示的数据。
- 整个结构存在这样的三层：dataLists(原底层数据)--Adapter--AdapterView
	getItem()方法的存在可以直接利用Adapter来获取数据，而不需要获取底层dataLists的引用；
	getItemAtPosition()方法的存在可以直接利用AdapterView 获取底层数据，而不需要获取其Adapter的引用。

5. getItemId(int position)
- getItemId()和getItemIdAtPosition()都提供了编程上面的便利。但是目前来看，由于对id没啥需求，所以大部分在重写getItemId方法时都是直接返回的position值。
- 但不要被这个做法所限制，而以为ItemId就是item在数据中的position。若有需求，可以利用getItemId()方法返回一些其他的值，比如每个item数据在数据库中id值，或者每个人的身份证号等。
