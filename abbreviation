## ORM或O/RM或O/R mapping--Object Relational Mapping--对象关系映射 ##

## IoC--Inversion of Control--控制反转
- 借助于“第三方”实现具有依赖关系的对象之间的解耦,控制权由应用代码中转到了外部容器
- 控制反转是Spring框架的核心。其原理是基于面向对象(OO)设计原则。
- 所有的组件都是被动的，所有的组件初始化和调用都由容器负责。组件处在一个容器当中，由容器负责管理。

- 引入IoC容器之前，对象A依赖对象B，那么A对象在实例化或者运行到某一点的时候，须主动创建对象B或者使用已有对象B，其控制权都在我们手上或者说应用代码中。
- 引入Ioc容器之后，对象A和对象B之间失去了直接联系，所以，当对象A实例化和运行时，如果需要对象B的话，IoC容器会主动创建一个对象B注入到对象A所需要的地方。
 
## AOP--Aspect Oriented Programming--面向切面编程 ##

### 切面（Aspect） ###
- Aspect 声明类似于 Java 中的类声明，在 Aspect 中会包含着一些 Pointcut 以及相应的 Advice。 

		例:声明一个切面 	
		@Aspect
		@Component
		public class BuyAspectJ {
		}

### Joint point（连接点） ###
- 切面逻辑程序执行的某个具体特定位置,理解为切面逻辑与业务逻辑进行连接的地方,如:类开始初始化前、类初始化后、类某个方法调用前、调用后、方法抛出异常后。
- Spring仅支持方法的连接点，即仅能在方法调用前、方法调用后、方法返回值时、方法抛出异常时以及方法调用前后这些程序执行点织入增强。
- 连接点由两个信息确定：第一是用方法表示的程序执行点即Pointcut；第二是用相对点表示的方位即Advice。

### 切点(Pointcut) ###
- 切面逻辑将要发生或插入的点,Spring AOP只针对方法

		例:@Pointcut("execution(* com.sharpcj.aopdemo.test1.IBuy.buy(..))")
    	public void point(){}
- Target（目标对象）：织入 Advice 的目标对象.。

### 引介(Introduction) ###

- 指在不更改源代码的情况，给一个现有类增加属性、方法，以及让现有类实现其它接口或指定其它父类等，从而改变类的静态结构。
- Spring AOP通过采代理加拦截器的方式来实现的，可以通过拦截器机制使一个现有类实现指定的接口。

###  通知（advice） ###
   		@Before：前置通知，在调用目标方法之前执行通知定义的任务
    	@After：后置通知，在目标方法执行结束后，无论执行结果如何都执行通知定义的任务
   		@After-returning：后置通知，在目标方法执行结束后，如果执行成功，则执行通知定义的任务
    	@After-throwing：异常通知，如果目标方法执行过程中抛出异常，则执行通知定义的任务
    	@Around：环绕通知，在目标方法执行前和执行后，都需要执行通知定义的任务。

    例:	@Before("point()")
	    public void hehe() {
	        System.out.println("before ...");
	    }

	注:与切点同时使用以确定切面逻辑的连接点,相当于:
	    @Before("execution(* com.sharpcj.aopdemo.test1.IBuy.buy(..))")
	    public void haha(){
	        System.out.println("男孩女孩都买自己喜欢的东西");
	    }
通知执行顺序:Before->Around->方法->Around->After->After-returning
