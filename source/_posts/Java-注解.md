---
title: Java注解系统学习
date: 2016-07-03 15:08:18
tags: java基础
---
   当初学习java的时候对注解只是一知半解，只知道一些简单的例如Override这样的注解。后来在学习其他框架中发现注解使用很多，对注解知识的缺乏促使我有必要好好的梳理一下这一知识点。
## 注解是什么
### 介绍注解
   解释注解是什么最合适的词就是元数据，元数据是只包含自己信息的数据。注解就是代码的元数据，他们包含了关于代码的信息。注解通常备用与包，类，方法，变量以及参数上，从java8之后注解可以几乎被用在代码的任何地方。注解不会影响到代码的逻辑，它们只是代码提供信息，第三方系统根据不同的目的可能会用到这些注解，也可能不会去用到。注解主要作用有以下方面：
   1.生成文档,通过代码里标识的元数据生成javadoc文档
   2.编译检查,通过代码里标识的元数据让编译器在编译期间进行检查验证
   3.编译时动态处理，编译时通过代码里标识的元数据动态代理,例如动态生成代码
   4.运行时动态处理,运行时通过代码里标识的元数据动态处理,例如使用繁盛注入实例
### 注解消费者
   在理解注解消费者之前，首先想一个问题，注解不包含任何方法逻辑，而且它们不会对被注解的代码产生影响，那么它们是怎么工作的呢,怎么才能体现出来上述它们的作用呢。
   这里提出一个注解消费者的概念，就是去解析被注解的代码，根据解析的注解信息来执行不同动作或者行为的系统或者应用。
   例如java 提供的内建的注解是被JVM来解析和执行的，那么JVM就是这些注解的消费者，再例如有些第三方框架提供的注解会被它们的处理器来解析，所以这些处理器就是那些注解的消费者，这部分会在后面有详细的说明

### 注解的语法
   通常注解是用@后面跟上注解名称来声明的例如
 ```
 @AnnotationClass
 public void annotatedMehod() {
 ...
 }
 ```
 这里就是对方法annotatedMethed()添加了一个AnnotationClass的注解,然后看一下AnnotationClass是如何定义的
 ```
 @Target(ElementType.METHOD)
 public @interface AnnotationClass {
 }
 ```
 可以看到注解是通过@interface 来创建的，和正常创建接口差不多,需要注意的是注解的修饰符只能是public或者abstract.可以看到AnnotationClass上面还有注解，这就是下面的环节 元注解
### 元注解 
  元注解是标记其他注解的注解,java提供的元注解主要有以下几个
  1.@Target 用来约束注解应该标记在什么地方,看源码 如下：
  ```
  @Documented
  @Retention(RetentionPolicy.RUNTIME)
  @Target(ElementType.ANNOTATION_TYPE)
  public @interface Target {
    /**
     * Returns an array of the kinds of elements an      annotation type
     * can be applied to.
     * @return an array of the kinds of elements an annotation type
     * can be applied to
     */
    ElementType[] value();
}
  ```
  可以看出Target也被其他元注解标注。返回的是一ElementType的数组，看一下这个ElementType类
  ```
  public enum ElementType {
    /** Class, interface (including annotation type), or enum declaration */
    TYPE,

    /** Field declaration (includes enum constants) */
    FIELD,

    /** Method declaration */
    METHOD,

    /** Formal parameter declaration */
    PARAMETER,

    /** Constructor declaration */
    CONSTRUCTOR,

    /** Local variable declaration */
    LOCAL_VARIABLE,
    
    /** Annotation type declaration */
    ANNOTATION_TYPE,
    
    /** Package declaration */
    PACKAGE,

    /**
     * Type parameter declaration
     *
     * @since 1.8
     */
    TYPE_PARAMETER,

    /**
     * Use of a type
     *
     * @since 1.8
     */
    TYPE_USE
}
  ```
  ElementType是枚举类型,其中的常量约束了注解应该标记的地方,因为@Target 返回的是枚举的数组类型,因此在指定值时应该是
 @Target(value= {ElementType.METHOD,ElementType.ANNOTATION_TYPE})
 这样的value的值用{}包括起来,中间用逗号隔开,其中value就是@Target返回值的变量,如果只指定一个值可以直接 @Target(ElementType.ANNOTATION_TYPE) 如果为指定具体的值,直接可以写成@Target,未指定值时相当于没有约束Target,这样的注解可以标注在任何元素上除了TYPE_PARAMETER
 2.@Retention 用来标注注解的的滞留时长，也就是注解的生命周期,其源码是这样的
 ```
 @Documented
 @Retention(RetentionPolicy.RUNTIME)
 @Target(ElementType.ANNOTATION_TYPE)
 public @interface Retention {
    /**
     * Returns the retention policy.
     * @return the retention policy
     */
    RetentionPolicy value();
}
 ```
 返回的是一个RetentionPolicy的值,看一下RetentionPolicy
```
   public enum RetentionPolicy {
    /**
     * Annotations are to be discarded by the compiler.
     */
    SOURCE,

    /**
     * Annotations are to be recorded in the class file   by the compiler
     * but need not be retained by the VM at run time.  This is the default
     * behavior.
     */
    CLASS,

    /**
     * Annotations are to be recorded in the class file by the compiler and
     * retained by the VM at run time, so they may be read reflectively.
     *
     * @see java.lang.reflect.AnnotatedElement
     */
    RUNTIME
}
```
RetentionPolicy是注解的滞留策略,其中的常量代表了注解滞留的生命周期,源码中的注释很清晰明了的说明了这一切,值得提的一点，前面说的注解的作用的时候,每个作用其实会对应每个滞留策略，这个在后面会详细的讲解
   3.@Inherited


 
  
  




### 内建注解  
   


## 注解怎么用






### 自定义注解

### 注解解析





