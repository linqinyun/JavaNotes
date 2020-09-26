# 多态

## 多态的概念

## 多态的实现

### 多态的场景使用及初步实现

### 向上转型

### 向下转型

### instanceof 运算符

### 类型转换总结

### 转换案例

## 抽象类

### 抽象类

### 抽象方法

## 接口

### 接口的定义

### 接口成员--抽象方法&常量

### 接口成员--默认方法&静态方法

### **关于多接口中重名默认方法处理的解决方案**

### **关于多接口中重常量处理的解决方案**

### 接口的继承

## 内部类

### 概述

### 成员内部类

### 静态内部类

### 方法内部类
### 匿名内部类1
--------------------
>对某个类的实例只会使用一次，类对于整个程序可有可无，可以将类的定义与类的创建，放到一起完成，简化程序。这种没有名字的类称为匿名内部类。  
通常情况下，通过匿名内部类简化抽象类与接口的操作

```
personTest.getRead(new Person() {
  @Override
  public void read() {
    // TODO Auto-generated method stub
    System.out.println("男生喜欢看科幻类的书籍");
  }
});
```
**适用场景:**
  - 只用到类的一个实例
  - 类到定义后马上使用
  - 给类命名并不会导致代码更容易理解
### 匿名内部类2
--------------------
**注意**  
1. 匿名内部类没有类型名称、实例对象名称
2. 编译后的为文件命名：外部类$数组.class
3. 无法使用private,protected,public,abstract,static修饰符 
4. 无法编写构造方法，可以添加构造代码块
5. 不能出现静态成员，不能出现抽象方法
6. 匿名内部类可以实现接口也可以继承父类，但是不可兼得
### 匿名内部类案例
- interface Ball接口
```
package pers.java.Ball;

public interface Ball {
	public void paly();
}
```
- BallTest 接口实现类
```
package pers.java.Ball;

public class BallTest {
	public BallTest() {
		
	}
	public void palyBall(Ball ball) {
		ball.paly();
	}
	public Inner_m getInnerM() {
		return new Inner_m();
	}
	//成员内部类
	class Inner_m implements Ball{
		@Override
		public void paly() {
			// TODO Auto-generated method stub
			System.out.println("成员内部类：");
			System.out.println("打篮球");
		}
	}
	//方法内部类
	public Object info() {
		class Inner_m implements Ball{
			@Override
			public void paly() {
				// TODO Auto-generated method stub
				System.out.println("**********");
				System.out.println("方法内部类:");
				System.out.println("打乒乓球");
			}
		}
		new Inner_m().paly();
		return null;		
	}
}

```
- test
```
package pers.java.Ball;

public class Test {
	public static void main(String[] args) {
		BallTest.Inner_m innerm = new BallTest().new Inner_m();
		innerm.paly();
		BallTest test = new BallTest();
		test.info();
		test.palyBall(new Ball() {
			@Override
			public void paly() {
				// TODO Auto-generated method stub
				System.out.println("**********");
				System.out.println("匿名内部类:");
				System.out.println("打排球");
			}
		});
	}
}

```
## 总结

1. 编译时多态（设计时多态）：方法重载
2. 运行时多态：JAVA运行时系统根据调用该方法的实例的类型来决定选择调用哪个方法则被称为运行时多态
* 通常指的多态，多指运行时多态
- 向上转型（Upcast）：将子类型转换为父类型。  
隐式/自动类型转换，是小类型到大类型的转换
- 向下转型（Downcast）：将父类型转换为子类型。  
强制类型转换，是大类型到小类型
- 通过instanceof运算符，来解决引用对象的类型，避免类型转换的安全性问题，提高代码的强壮性。
------
抽象类
1. 抽象类不能直接实例化
2. 子类如果没有重写父类所有的抽象方法，则也要定义为抽象类
3. 抽象方法所在的类一定是抽象类
4. 抽象类中可以没有抽象方法
------
接口
- 接口定义了某一批类所需要遵守的规范
- 接口不关系这些类的内部数据，也不关心这些类里方法的实现细节，它只规定这些类里必须提供某些方法  
**语法**  
```
[修饰词] interface 接口名 [extends 父接口1，父接口2...]
{
  零个到多个常量定义...
  零个到多个抽象方法的定义...
  零个到多个默认方法的定义...(jdk1.8新增)
  零个到多个静态方法的定义...(jdk1.8新增)
}
```
**注意**  
- 接口可以实现多继承，即一个子接口可以同时继承多个父接口
- 实现接口的类如果不能实现所有接口中待重写的方法，则必须设置为抽象类
- 一个类可以继承自一个父类，同时实现多个接口
------
内部类  
- 在Java中，可以将一个类定义在另一个类里面或者一个方法里面，这样的类称为内部类
- 与之对应，包含内部类的类也被称为外部类  
    - 成员内部类
    - 静态内部类
    - 方法内部类
    - 匿名内部类
- 优势  
内部类中提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一包中的其他类访问该类，更好的实现了信息隐藏。注意访问规则

## 案例
### 马戏团节目管理  
**整个项目由三个环节组成**
 - 表演菜单展示
 - 选择表演者进行表演
 - 选择是否继续观看表演  
### 详细设计
- 抽象父类
	- 动物（Animal）
		- 属性：昵称（name），年龄（age）
		- 抽象方法：描述喜好（love）
- 接口
	- 表演（IACT）
		- 抽象方法：描述技能（skill），描述表演（act）  
		每个表演者的表演信息是通过调用act方法输出的
- 实现类
	- 棕熊（Bear）
		- 继承Animal实现IACT
	- 狮子（Lion）
		- 继承Animal实现IACT
		- 新增属性：颜色（color）、性别（sex）
	- 猴子（Monkey）
		- 继承自Animal实现IACT
		- 新增属性：品种（type）
	- 鹦鹉（parrot）
		- 继承Animal是实现IACT
		- 新增属性：品种（type）
	- 小丑（clown）
		- 实现IACT
		- 属性：名字（name）、艺龄（years）
		- 新增方法：着装特点（dress）