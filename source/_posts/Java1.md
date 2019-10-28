---
title: Java基础①
top: false
cover: false
toc: true
mathjax: true
date: 2019-10-27 17:30:46
password:
summary:
tags:
- Java
- 基础
categories:
- Java
---

# Java面向对象
---
## 对象和封装

1. 当一个对象作为参数，传递到方法中时，实际上传递的是地址值。
2. **局部变量、成员变量区别**

* 定义的位置不一样(**重点**)
局部：在方法的内部。
成员：在方法的外部，直接写在类当中。

* 作用范围不一样(**重点**)
局部：只在方法当中才有用，出了方法就不能用了。
成员：整个类都能使用。

* 默认值不同(**重点**)
局部：没有默认值，要想用，必须手动赋值。
成员：如果没有赋值，会有默认值，规则和数组一样。

* 内存的位置不一样(了解)
局部：位于栈内存。
成员：位于堆内存。

* 生命周期不一样
局部：随着方法进栈而诞生，随着方法的出栈而消失。
成员：随着对象创建而诞生，随着对象被垃圾回收而消失。

3. 封装就是将一些细节信息隐藏起来，对外界不可见。

4. 构造方法是专门用来创建对象的方法，当我们利用关键字new来创建对象时，其实就是调用的构造方法。格式如下：
```java
//无参构造方法
public class_name(){
	方法体
}
//有参构造方法
public class_name(type name){
	方法体
}
```

## 继承
1. 在继承中，“子类就是一个父类”，就是说子类可以被当成一个父类看待。
```java
//父类格式：
public class Fu_class{
	...
}
//子类格式：
public class Zi_class extends Fu_class{
	...
}
```
在子类中，访问变量的方式如下：
```java
局部变量：name
本类成员变量：this.name
父类成员变量：super.name
```
2. 重写(\(override\)):在继承关系中，方法名称一样，参数列表也**一样**。
   重载(\(overload\)):方法名称一样，参数列表**不一样**。
   
3. 重写注意事项：
* 必须保证父子类之间的名称相同，参数列表也相同,利用`@Override`来检测是不是有效的覆盖重写
```java
@Override
public void name(type parameter_name){
	方法体
}
```
* 子类方法的返回值必须**小于等于**父类方法的返回值范围
* 子类方法的权限必须**大于等于**父类方法的权限修饰符
```java
public > protected > (default) > private
//default指的是留空，不写
```

4. 继承关系中，父类构造方法的访问特点：
子类必须调用父类构造方法，不写则赠送一个`super()`方法，写了则用指定的super调用，super只能有一个，还必须是第一个。

5. 继承中super关键字的用法有3种：
* 在子类的**成员方法**中，访问父类的**成员变量**。
* 在子类的**成员方法**中，访问父类的**成员方法**。
* 在子类的**构造方法**中，访问父类的**构造方法**。

## 抽象

1. 抽象方法：在权限修饰符后加上`abstract`关键字，去掉大括号，分号结束。
```java
public abstract void method_name ();
```
2. 抽象类：在class前加上`abstract`即为抽象类。
```java
public abstract class class_name{
	...
}
```

3. 使用抽象类和抽象方法：
* 不能直接`new`（创建）抽象类对象
* 必须用一个子类来继承抽象父类
* 子类必须覆盖重写（去掉`abstract`关键字，写方法体）抽象父类中的所有抽象方法
* 创建子类对象进行使用

## 接口（Interface）


1. 接口使用步骤：
* 建立一个`Interface`类，里边写抽象方法
```java
public Interface Interface_name{
	...
}

* 接口不能直接使用，必须有一个“实现类”来“实现”该接口
```java
public class imp_name implements Interface_name{
	...
}
```

* 接口的实现类必须覆盖重写（实现）接口中**所有**的抽象类

* 创建实现类的对象，进行使用

2. 接口中定义"成员变量"，使用`public static final`进行修饰，格式：
```java
//其中public static final可以省略，但是不写，默认也是这样
public static final type var_name = value;
```

3. 类-接口：
* 类与类之间是单继承，直接父类只有一个
* 类与接口之间是多实现的，一个类可以实现多个接口
* 接口与接口之间是多继承的
* 多个父接口之间当中的抽象方法如果重复，没有关系
* 多个父接口当中的默认方法（`defaule`关键字）如果重复，那么子接口必须进行默认方法的重写

## 多态

1. 其实就是一句话：父类引用指向子类对象，格式：
```java
Fu_class obj = new Zi_class();
//or
Interface_name obj = new implements_name();
```

2. 多态下成员变量、成员方法使用口诀：
* 成员变量：编译看左边，运行看左边
* 成员方法：编译看左边，运行看右边

3. 对象的转型
* 对象的向上转型，其实就是多态写法，格式：
```java
Fu_class obj = new Zi_class();
```
* 对象的向下转型，其实就是[**还原**]动作，格式：
```java
Zi_class obj = (Zi_class) Fu_obj_name();
```

* `instance of`会得到一个`boolean`值结果，判断前边的对象能不能作为后边类型的实例
```java
obj instance of class_name;
```

## 四种权限修饰符
```java
                    public  >   protected  >  (default)  >  private
同一个类(我自己)       √            √             √            √
同一个包(我领居)       √            √             √            ×
不同包子类(我儿子)     √            √             ×            ×
不同包非子类（陌生人） √            ×             ×            ×
```