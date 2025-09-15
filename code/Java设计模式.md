# 基础
## 分类
1. 创建型模式：提供创建对象的机制，提升已有代码的灵活性和可复用性
2. 结构型模式：介绍如何将对象和类组装成较大的结构，并同时保持结构的灵活和高效
3. 行为模式：负责对象间的高效沟通和职责传递委派
# 六大设计原则
## 单一职责原则
Single Responsibility Principle, SRP，又称单一功能原则，面向对象的五个基本原则（SOLID）之一
一个类应只有一个发生变化的原因
## 开闭原则
- Open-Close Principle，OCP
- 对象、类、模块和函数对扩展应该开放，但对修改应封闭；
- 应该用抽象定义结构，用具体实现扩展细节
- 即面向抽象编程
## 里氏替换原则
- 继承必须确保超类所具有的性质在子类中仍然成立
- 即：子类可以扩展父类的功能，但不能改变弗雷原有的功能
	- 子类可以实现父类的抽象方法，但不能覆盖父类的非抽象方法
	- 子类可以增加自己特有的方法
	- 当子类的方法重载父类的方法时，方法的前置条件要比父类的方法更宽松
	- 当子类的方法实现父类的方法时，方法的后置条件要比父类的方法更严格活与父类方法相等
## 迪米特法则原则
- Law of Demeter，LoD，又称最少知道原则（Least Knowledge Principle，LKP）
- 一个对象类对于其他对象类而言，知道的越少越好
- 有内在关联的类要内聚，没有直接关系的类要低耦合
## 接口隔离原则
- Interface Segregation Principle，ISP
- 客户端不应该被迫依赖于它不使用的方法
	- 一个类对另一个类的依赖应该建立在最小的接口上
- 规则
	- 接口尽量小但有限度，一个接口只服务于一个子模块活业务逻辑
	- 为依赖接口的类定制服务，只提供调用者需要的方法，屏蔽不需要的方法
	- 根据业务逻辑进行接口拆分
	- 提高内聚，减少对外交互。让接口使用最少的方法完成最多的事情
## 依赖倒置原则
- Dependence Inversion Principle，DIP
- 设计代码架构时，高层模块不应依赖于底层模块，两者均应依赖于抽象
- 抽象不应依赖于细节，细节应依赖于抽象
# 工厂模式
- 也称简单工厂模式，是创建型设计模式的一种
- 提供了按需创建对象的最佳方式
- 不会对外暴露创建细节，并会通过一个统一的接口创建所需对象
- 将创建过程延迟到子类中进行
# 抽象工厂模式
- 工厂的工厂，属于创建型模式
## 建造者模式
- 相同物料，不同的组装方式
# 原型模式
- 创建重复对象，而对象内容本身比较复杂，或比较耗时，应采用复制的方式节省时间 
## 单例模式
- 保证一个类只有一个实例，并需提供一个全局访问该实例的点
### 七种单例模式实现方式
#### 静态类使用
```java
public class Singleton_00 {
	public static Map<String,String> cache = new ConcurrentHashMap<String,String>();
}
```
- 用于无需维持任何状态，仅用于全局访问
#### 懒汉模式（线程不安全）
```java
public class Singleton_01 {
	private static Singleton_01 instance;
	private Singleton_01() {
	}
	public static Singleton_01 getInstance() {
		if (null != instance) return instance;
		instance = new Singleton_01();
		return instance;
	}
}
```
- 在默认的构造函数上添加了私有属性private
- 当多个访问者同时获取对象实例时，会造成多个同样的对象实例并存
#### 懒汉模式（线程安全）
```java
public class Singleton_02 {
	private static Singleton_02 instance;
	private Singleton_02() {
	}
	public static synchronized Singleton_02 gitInstance() {
		if (null!=instance) return instance;
		instance = new Singleton_02();
		return instance;
	}
}
```
- 使用`synchronized`关键字进行加锁，线程安全，但是所有访问因为需要锁占用，造成资源浪费
#### 饿汉模式（线程安全）
```java
public class Singleton_03 {
	private Singleton_03 instance = new Singleton_03();
	private Singleton_03() {
	}
	private static Singleton_03 getInstance() {
		return instance;
	}
}
```
- 非懒加载
### 使用类的内部类（线程安全）
```java
public class Singleton_04 {
	private static class SingletonHolder {
		private static Singleton_04 instance = new Singleton_04();
	}
	private Singleton_04() {
	}
	public static getInstance() {
		return SingletonHolder.instance;
	}
}
```
- 懒加载，且线程安全，并且不会因为加锁而降低性能
- 因为JVM虚拟机可以保证多线程并发访问的正确性，即一个类的构造方法在多线程环境下可以被正确的加载
#### 双重锁校验（线程安全）
```java
public class Singleton_05 {
	private static volatile Singleton_05 instance;
	private Singleton_05() {
	}
	public static Singleton_05 getInstance() {
		if (null != instance) return instance;
		synchronized (Singleton_05.class) {
			if (null == instance) {
				instance = new Singleton_05;
			}
		}
		return instance;
	}
}
```
### CAS "AtomicReference"（线程安全）
```java
public class Singleton_06 {
	private static final AtomicReference<Singleton_06> INSTANCE = new AtomicReference<Singleton_06>();
	private static Singlenton_06 instance;
	private Singlenton_06() {
	}
	public static final Singleton_06 getInstance() {
		for (;;) {
			Singleton_06 instance = INSTANCE.get();
			if (null != instance) return instance;
			INSTANCE.compareAndSet(null, new Singleton_06());
			return INSTANCE.get();
		}
	}
}
```
- Java并发库提供了很多原子类，支持并发访问的数据安全性，如：AtomicInteger、AtomicBoolean、AtomicLong和AtomicReference
- `AtomicReference<V>`可以封装一个实例
- 依赖CAS的忙等算法、底层硬件的实现保证线程安全
#### 枚举单例（线程安全）
```java
public enum Singleton_08 {
	INSTANCE;
	public void test() {
		System.out.println("hi");
	}
}
```
# 适配器模式
- 把原本不兼容的接口通过适配修改做到统一，方便调用方使用
- 不仅可以适配接口，还可适配属性信息
# 桥接模式
- 通过将抽象部分与实现部分分离，将多种可匹配的使用进行组合
- 在A类中含有B类接口，通过构造函数传递B类的实现