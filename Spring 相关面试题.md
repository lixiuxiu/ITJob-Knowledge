#  Spring 相关

## 1.静态代理和动态代理

代理模式是java常用的设计模式之一，他就是将对一个对象的直接访问变为访问这个对象的代理对象，通过这个代理对象来间接的访问和增强原来的对象。

### 1.1 为什么要有代理模式呢？

因为开闭原则的体现，一个良好的设计应该对修改关闭，对扩展开放，代理是为了扩展类而存在的。

### 1.2 静态代理

通过直接编写代理类来实现的代理被称为静态代理。静态代理要求我们在开发阶段就为目标类编写对应的代理类。他的优点是简单易行，执行效率高，但是缺点是是比较死板，工作量大，难以适应灵活多变的需求，如果是需要为多个类进行代理，并且代理类的功能是一致的，那么我们需要为每一个具体类实现一个代理类，就会很麻烦.

### 1.3 动态代理

动态代理是动态的生成具体委托类的代理类对象。与静态代理不同的是，动态代理不需要为各个委托类逐一实现代理类，而是为一类代理类写一个具体的实现类就行了。

### 1.4 java常用的两种动态代理的模式

#### （1）JDK动态代理

 JDK自带的创建动态代理的API帮助我们在程序运行时从内存中动态的生成并装载代理类的字节码。jdk的java.lang.reflect.proxy类的newProxyInstance()方法可以为我们动态生成（实现了指定接口的）代理对象。我们需要实现InvocationHandler接口的类实现代理逻辑。

#### （2）CGLIB动态代理

CGlib动态代理通过（动态字节码技术）为一个目标类创建子类，然后在子类中覆盖父类的方法，加入自己的处理逻辑。

#### （3）JDK动态代理 VS CGLIB动态代理

CGlib创建的动态代理对象在性能方面要比JDK创建的动态代理对象要高不少，但是创建代理对象花费的时间比JDK动态代理多的多，所以对于一次创建多次使用的对象用GClib更合适，反之，用JDK动态代理

## 2.IOC和DI

### 2.1 IOC作用

用来减低计算机代码之间的耦合度。

### 2.2 IOC-控制反转

是对组件对象控制权的转移。是把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。

### 2.3 DI

IOC中最常见的方式叫做**依赖注入**，例如：Class A中用到了Class B的对象b，一般情况下，需要在A的代码中显式的new一个B的对象。采用依赖注入技术之后，A的代码只需要定义一个私有的B对象，不需要直接new来获得这个对象，而是通过相关的容器控制程序来将B对象在外部new出来并注入到A类里的引用中。

根据@Autowaired注解，ioc容器会根据类型或者名称去找到对应的类。

### 2.4 依赖注入的方式

Spring支持setter注入和构造器注入，通常使用构造器注入来注入必须的依赖关系，对于可选的依赖关系，则setter注入是更好的选择，setter注入需要类提供无参构造器或者无参的静态工厂方法来创建对象。总之，把要注入的抽象接口new出来的对象放在外面传入进来，那就不用依赖具体的实现类。

#### （1）构造器注入

```java
public class UserService{
	//创建dao接口引用指向实现类对象--直接创建对象
	private UserDao userDao;
	//使用有参构造方法
	public UserService(UserDao userDao){
		this.userDao=userDao;
	}
}
```

#### （2）setter注入

同样的，我们也可以使用增加一个setter的方式来传入一个创建好的UserDaoImpl对象

```java
public class UserService{
	//创建dao接口引用指向实现类对象--直接创建对象
	private UserDao userDao;
	public void setUserDao(UserDao userDao){
			this.userDao=userDao;
	}
}
```

####  (3）接口注入

接口注入是使用接口来提供setter方法，首先得创建一个接口

```java
public interface InjectDao{
	void injectDaoImpl(UserDao userDao);
}
```


然后让UserService实现该接口

```java
public class UserService implements InjectDao{
	//创建dao接口引用指向实现类对象--直接创建对象
	private UserDao userDao;
	public void injectDaoImpl(UserDao userDao){
			this.userDao=userDao;
	}
```

IoC中最基本的Java技术就是“反射”编程。通俗的说，反射就是根据给出的类名（字符串）来生成对象。这种编程方式可以让应用在运行时才动态决定生成哪一种对象。



## 3.反射

反射可以让我们在运行时获取类的属性，方法，构造方法、父类、接口等信息，通过反射还可以让我们在运行期实例化对象、调用方法、即使方法或属性是私有的的也可以通过反射的形式调用

想在运行时使用类型信息，必须获取对象(比如类Base对象)的Class对象的引用，使用功能Class.forName(“Base”)可以实现该目的，或者使用base.class。注意，有一点很有趣，使用功能”.class”来创建Class对象的引用时，不会自动初始化该Class对象，使用forName()会自动初始化该Class对象。为了使用类而做的准备工作一般有以下3个步骤：

- 加载：由类加载器完成，找到对应的字节码，创建一个Class对象
- 链接：验证类中的字节码，为静态域分配空间
- 初始化：如果该类有超类，则对其初始化，执行静态初始化器和静态初始化



## 4.AOP

AOP称为面向切面编程，将约定利用动态代理的技术织入到相应的流程中去。

### AOP用处

在程序开发中主要用来解决一些系统层面上的问题，比如日志，事务，权限等待，Struts2的拦截器设计就是基于AOP的思想，是个比较经典的例子。

### AOP的基本概念

 **将通知织入到切入点指定的连接点处**。

(1)Aspect(切面):通常是一个类，里面可以定义切入点和通知

(2)JointPoint(连接点):程序执行过程中明确的点，一般是方法的调用

(3)Advice(通知):AOP在特定的切入点上执行的增强处理，有before,after,afterReturning,afterThrowing,around

(4)Pointcut(切入点):就是带有通知的连接点，在程序中主要体现为书写切入点表达式

(5)AOP代理：AOP框架创建的对象，代理就是目标对象的加强。Spring中的AOP代理可以使JDK动态代理，也可以是CGLIB代理，前者基于接口，后者基于子类

### Spring AOP

Spring中的AOP代理还是离不开Spring的IOC容器，代理的生成，管理及其依赖关系都是由IOC容器负责，Spring默认使用JDK动态代理，在需要代理类而不是代理接口的时候，Spring会自动切换为使用CGLIB代理，不过现在的项目都是面向接口编程，所以JDK动态代理相对来说用的还是多一些。

### 通知类型介绍

(1)Before:在目标方法被调用之前做增强处理,@Before只需要指定切入点表达式即可

(2)AfterReturning:在目标方法正常完成后做增强,@AfterReturning除了指定切入点表达式后，还可以指定一个返回值形参名returning,代表目标方法的返回值

(3)AfterThrowing:主要用来处理程序中未处理的异常,@AfterThrowing除了指定切入点表达式后，还可以指定一个throwing的返回值形参名,可以通过该形参名

来访问目标方法中所抛出的异常对象

(4)After:在目标方法完成之后做增强，无论目标方法时候成功完成。@After可以指定一个切入点表达式

(5)Around:环绕通知,在目标方法完成前后做增强处理,环绕通知是最重要的通知类型,像事务,日志等都是环绕通知,注意编程中核心是一个ProceedingJoinPoint

## 5.bean的生命周期

![image-20190417150741810](https://ws4.sinaimg.cn/large/006tNc79ly1g25nbgsl46j30yk0u04qp.jpg)

## 6.spring的模块

![image-20190417151030355](https://ws4.sinaimg.cn/large/006tNc79ly1g25ne9vf7xj310u0ji42r.jpg)

Core包是框架的最基础部分，并提供依赖注入（Dependency Injection）管理Bean容器功能。

Context包，构建于Core包上，提供了一种框架式访问对象的方式，有些像JNDI注册。Context封装包继承了beans包的功能，还增加了国际化（I18N）,事件传播，资源装载，以及透明创建上下文，例如通过servlet容器。

DAO包提供了JDBC的抽象层，它可消除冗长的JDBC编码和解析数据库厂商特有的错误代码。并且，JDBC封装包还提供了一种比编程性更好的声明性事务管理方法，不仅仅是实现了特定接口，而且对所有的POJOs都适用。

ORM包为流行的“关系/对象”映射APIs提供了集成层，包括JDO，hibernate和iBatis。通过ORM包，可以混合使用所有Spring提供的特性进行“对象/关系”映射，如前边提到的简单声明性事务管理。

AOP包提供了符合AOP Alliance规范的面向方面的编程实现，例如方法拦截器（method-interceptors）和切点（pointcuts），从逻辑上讲，从而减弱代码的功能耦合，清晰的被分离开。

Web包提供了基本的面向Web的综合特性，例如多方文件上传，利用Servlet listeners进行IoC容器初始化和针对Web的applicationcontext。当与WebWork或Struts一起使用Spring时，这个包使Spring可与其他框架结合。

Web MVC提供了面向Web应用的Model-View-Controller实现。Spring的MVC框架并不是仅仅提供一种传统的实现，它提供了一种清晰的分离模型，在领域模型代码和web form之间。并且，还可以借助Spring框架的其他特性。