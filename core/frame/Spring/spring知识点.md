# 1.IOC相关

1.IOC：Inversion of Control，翻译为 “控制反转”，它还有一个别名为 DI（Dependency Injection）,即依赖注入。

2.控制反转：原来传统开发模式下都是直接由我们new对象，也就是自己所依赖的对象由自己控制，但有了 IOC 之后都是 IOC 容器来帮我们创建对象

3.依赖注入：顾名思义在将对象注入到 IOC 容器的时候还有该对象的依赖也需要同时注入到容器之中，本质来向 IOC 和 DI 是一个概念

4.依赖注入的方法

* 基于构造函数注
* 基于 setter 注入

4.1.1基于构造函数注入

```plain
<beans>
   <bean id="textEditor" class="com.tutorialspoint.TextEditor">
      <constructor-arg ref="spellChecker"/>
   </bean>
   <!-- Definition for spellChecker bean -->
   <bean id="spellChecker" class="com.tutorialspoint.SpellChecker">
   </bean>
</beans>
```
4.1.2基于构造函数参数类型注入
```plain
<beans>
   <bean id="exampleBean" class="examples.ExampleBean">
      <constructor-arg type="int" value="2001"/>
      <constructor-arg type="java.lang.String" value="Zara"/>
   </bean>
</beans>
```
4.1.3基于构造参数索引注入(index 从0开始)
```plain
<beans>
   <bean id="exampleBean" class="examples.ExampleBean">
      <constructor-arg index="0" value="2001"/>
      <constructor-arg index="1" value="Zara"/>
   </bean>
</beans>
```
# 2.Bean

1.Bean 定义： bean 的对象是构成应用程序的支柱也是由 Spring IoC 容器管理的。bean 是一个被实例化，组装，并通过 Spring IoC 容器所管理的对象。

2.Bean 的属性

|**属性**|**描述**|
|:----|:----|
|class|这个属性是强制性的，并且指定用来创建 bean 的 bean 类|
|name|这个属性指定唯一的 bean 标识符。在基于 XML 的配置元数据中，你可以使用 ID 和/或 name 属性来指定 bean 标识符。|
|scope|这个属性指定由特定的 bean 定义创建的对象的作用域|
|constructor-arg|它是用来注入依赖关系的|
||properties它是用来注入依赖关系的|
|autowiring mode|它是用来注入依赖关系的|
|lazy-initialization mode|延迟初始化的 bean 告诉 IoC 容器在它第一次被请求时，而不是在启动时去创建一个 bean 实例。|
|initialization 方法|在 bean 的所有必需的属性被容器设置之后，调用回调方法。|
|destruction 方法|当包含该 bean 的容器被销毁时，使用回调方法。|
|abstract|true 设置为抽象 bean 模板|
|parent|继承注入 可以抽象出一个公共的bean模板，让子类去继承|

3.Spring 配置元数据方式

* 基于 XML 的配置文件
* 基于注解的配置
* 基于Java 的配置

4.Bean 的作用域属性（scope）

|**作用域**|**描述**|
|:----|:----|
|singleton|该作用域将 bean 的定义的限制在每一个 Spring IoC 容器中的一个单一实例(默认)。|
|prototype|该作用域将单一 bean 的定义限制在任意数量的对象实例。|
|request|该作用域将 bean 的定义限制为 HTTP 请求。只在 web-aware Spring ApplicationContext 的上下文中有效。|
|session|该作用域将 bean 的定义限制为 HTTP 会话。 只在web-aware Spring ApplicationContext的上下文中有效。|
||global-session该作用域将 bean 的定义限制为全局 HTTP 会话。只在 web-aware Spring ApplicationContext 的上下文中有效。|

5.Bean 的生命周期

* BeanPostProcessor#before 后置处理器
* 初始化
* BeanPostProcessor#after
* 销毁

初始化回调：

1.当前对象实现 InitlaizingBean 重写 afterPropertiesSet()方法

```plain
public class ExampleBean implements InitializingBean {
   public void afterPropertiesSet() {
      // do some initialization work
   }
}
```
2.XML 配置元数据可以使用 init-method 属性指定带有 void 无参方法的名称
```plain
<bean id="exampleBean" 
         class="examples.ExampleBean" init-method="init"/>
```
销毁回调：
1.当前对象实现 DisposableBean 重写 destroy() 方法

```plain
public class ExampleBean implements DisposableBean {
   public void destroy() {
      // do some destruction work
   }
}
```
2.XML 配置元数据可以使用 destroy-method 属性指定带有 void 无参方法的名称
```plain
<bean id="exampleBean" class="examples.ExampleBean" destroy-method="destroy"/>
```
这个流程是对每个 Bean 来说的
BeanPostProcessor#postProcessBeforeInitalization -> 初始化

-> BeanPostProcessor#postProcessAfterInitalization -> 实例化 -> 销毁

