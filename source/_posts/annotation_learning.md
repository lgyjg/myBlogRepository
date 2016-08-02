---
layout:     post
title: java 中的注解
subtitle:   针对java中注解的学习笔记
date: 2016-08-02 20:22:04
author:     "JianGuo Yang"
header-img: 
tags: Java
---
> 一直对java中的注解不是很了解，但是随处可见，前些天，一位朋友@徐文志程序猿在博客中写了关于PHP的注释，学习了很多，所以，也尝试着学习下java中的注解，并记录在这里，供以后复习，也便于大家共同学习。


在开始之前，我墙裂给大家安利一种学习方式。思维导图，又称脑图，是能够将思维中抽象的逻辑关系转化为直观的关系图标的一种方式，在我们的学习中，可以将知识点通过思维导图梳理出来，非常有条理，还方便记忆，这篇文章中，我会尝试着用思维导图阐述我的学习过程。好了现在就开始干正事，切入正题吧。

注解（Annotation）是java 5.0引入的新特性。它提供了一种结构化的类型检查的新途径。我们通过加入注解，能够避免很多问题，例如编写累赘的部署描述文件。与代码注释相比，它更注重与描述类的相关信息。
# 基本的语法
注解的语法还是比较简单的，除了多了@符号外，其他的和java的固有语法一致。
在java SE5 中就提供了三种原生的注解：
  * @Override 表示当前的方法继承自父类，并且复写了父类的方法，如果被注解的方法在父类中不存在，编译器就会抛出异常。在java中，这个注解是可选的。
  * @Deprecated 表示当前的方法已经被废弃，在编译时会有警告提示。
  * @SuppressWarings 表示主动忽略不恰当的编译器警告。
  此外，java 还提供了可扩展的annotation API。
  下面的例子说明了注解的使用：  


  ```java
public class Testable {
    public void execute(){
      System.out.println("Executing...");
    }
    @Test
    void testExecute (){
      execute();
    }
}
  ```
  **@Test** 注解本身不做任何的操作，但是，编译器在编译的时候，就必须找到关于该注解的定义，否则就会报错。下面的一小节将会介绍如何进行定义。

# 注解的定义
下面，我们就给出前文提到的@Test注解的定义：
```java
import java.lang.annotation

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Test{}
```
这样，就定义了一个@Test的注解。我们可以看到，其实和接口的定义很像。不同的是，在定义注解时，我们需要一些[元注解](#什么是元注解)，如@Target，@Retention。其中：  
* **@Target** 注解用来定义该注解的作用域，如作用于一个方法还是一个域。
* **@Retention** 则定义了该注解在哪个级别可用，源代码（SOURCE）中、类文件（CLASS）中、运行时（RUNTIME）。
这类注解由于没有元素，被称为 **标记注解（marker annotation）**， 通常情况下，注解还会加上一些元素用于表示某些值。这些值用于编译器在分析和处理该注解时的参考。可以为这些元素指定默认值。
我们来看看元素的使用：  

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface UseCase{
  public int id();
  public String description() default "no description";
}
```
这个@UserCase 注解就定义了两个元素，我们为description元素制定了默认值。如果使用该注解在注解某个方法时，没有给定描述字符，将会使用该默认值代替。下面我们接着看看如何使用该注解。

# 注解的使用
注解元素的使用过程中，是以键-值对的形式给出的。
```java
public class PasswordUtils {
  @UseCase(id= 1,description="Password must contain at least one numeric")
  public boolean validataPassword(String password) {
    return(password.mathes("\\w*\\d\\w*"))
  }

  @UseCase(id=2)
  public String encryptPassword(String password) {
    return new StringBuffer(password).reverse().toString();
  }

  @UseCase(id=3,description="New password can't equal previously password")
  public boolean checkForNewPassword(List<String> prePassWords, String password){
    return !prePassWords.contains(password);
  }

}
```

# 什么是元注解
我们知道，万物是有源头的，就像我们的大千世界都是由原子构成的。元注解就是注解的源头，用于注解其他的注解。这句话有点绕，其实就是在我们定义注解的时候，使用元注解来定义该注解的作用域，使用级别，是否允许继承该注解等相关属性。如下表：

| 元注解          | 解释     |
| :------------- | :------------- |
| @Target        |   表示该注解可以用于什么地方     |
| @Retention     |   表示在什么级别保存该注解信息     |
| @Documented    |   将此注解包含在javaDoc中     |
| @Inherited     |   允许子类继承父类的注解     |

其中@Target的取值有七种：  

| 值     | 解释     |
| :------------- | :------------- |
| CONSTRUCTOR       | 构造器的声明       |
| FIELD       | 域声明（包括enum）       |
| LOCAL_VARIABLE       | 局部变量的声明       |
| METHOD       | 方法的声明       |
| PACKAGE       | 包的声明       |
| PARAMETER     | 参数的声明       |
| TYPE       | 类，接口，或enum的声明       |

接下来将会学习编写注解解释器程序通过反射用于实现注解对应的功能。  
未完待续～
