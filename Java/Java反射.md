是在运行状态中，对于任意的一个类，都能够知道这个类的所有属性和方法，对任意一个对象都能够通过反射机制调用一个类的任意方法，
这种动态获取类信息及动态调用类对象方法的功能称为java的反射机制。

反射的作用：

1、动态地创建类的实例，将类绑定到现有的对象中，或从现有的对象中获取类型。

2、应用程序需要在运行时从某个特定的程序集中载入一个特定的类

详见：java反射机制原理

反射 一般使用 Class.forName()方法;

动态代理就是实现InvocationHandler 接口；

每个类都会产生一个对应的Class对象，也就是保存在.class文件。所有类都是在对其第一次使用时，动态加载到JVM的，当程序创建一个对类的静态成员的引用时，就会加载这个类。Class对象仅在需要的时候才会加载，static初始化是在类加载时进行的。 

类加载器首先会检查这个类的Class对象是否已被加载过，如果尚未加载，默认的类加载器就会根据类名查找对应的.class文件。

　　想在运行时使用类型信息，必须获取对象(比如类Base对象)的Class对象的引用，使用功能Class.forName(“Base”)可以实现该目的，或者使用base.class。注意，有一点很有趣，使用功能”.class”来创建Class对象的引用时，不会自动初始化该Class对象，使用forName()会自动初始化该Class对象。为了使用类而做的准备工作一般有以下3个步骤：

加载：由类加载器完成，找到对应的字节码，创建一个Class对象
链接：验证类中的字节码，为静态域分配空间
初始化：如果该类有超类，则对其初始化，执行静态初始化器和静态初始化块 

RTTI:Run-Time Type Identification 运行时类型信息
      能够使用基类的指针或引用来检查这些指针或引用所指的对象的实际派生类型。

mybatis
当抽象方法的参数超过1个时，必须添加@Param注解，并且，在XML配置中，使用#{}表示的变量的名称其实是@Param注解中的值！

 动态SQL
MyBatis中，在配置XML映射时，可以使用某些逻辑节点，实现逻辑判断或者循环等等，使得每次执行的SQL语句是可能随着参数发生变化的

SQL中，有2种占位符，分别使用#{}和${}，
前者，用于对值进行占位，可以替换在预编译的SQL语句中的?，在实际执行时，也是预编译的，所以，在使用#{}格式时，无须考虑参数的类型，
后者，用于对非值的语句部分进行占位，在实际执行时，是直接拼接到SQL语句中的，并不具备预编译的效果。

，MyBatis会将查询结果封装到对象中，其要求是查询结果中的列名(字段名)与实体类的属性名必须完全一致,在定义别名时，AS关键字并不是必须的，直接通过空格分隔原名和别名即可

如果尝试执行多表关联查询，必然没有匹配的实体类可以封装查询结果，则需要创建VO（Value Object）类，它不同于实体类，实体类是与某1张数据表完全对应的，而VO类是与实际应用需求相对应的！

resultMap
在查询时，<select>节点必须指定结果的类型，可以通过resultType属性来指定，也可以通过resultMap属性来指定。
当有直接对应的查询结果时，可以使用resultType，取值一般是实体类的类型，或VO类的类型。
某些查询可能需要将查询结果进行特殊的封装，例如查询时存在1对多、多对多、多对1等关系，则需要使用resultMap来配置封装的方式。

<resultMap id="Department_VO_Map" 
    type="cn.tedu.mybatis.vo.DepartmentVO">
    <!-- id节点：配置主键 -->
    <!-- column：查询结果中的列名 -->
    <!-- property：以上type属性对应的数据类型中的属性名 -->
    <id column="did" property="did"/>
    <!-- result节点：配置普通字段 -->
    <result column="name" property="name"/>
    <!-- collection节点：配置List集合类型的属性，用于1对多的查询 -->
    <!-- ofType：在List里放的是什么类型 -->
    <collection property="users"
        ofType="cn.tedu.mybatis.entity.User">
        <id column="uid" property="id"/>
        <result column="username" property="username"/>
        <result column="password" property="password"/>
        <result column="age" property="age"/>
        <result column="phone" property="phone"/>
        <result column="email" property="email"/>
        <result column="isDelete" property="isDelete"/>
    </collection>
</resultMap>
