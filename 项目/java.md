## static

### 类方法

类方法，用static写函数，直接.名字

实例方法，要new一个对象，占用堆内存

### 代码块

只运行一次

```java
static{
    
}
```

## extends

继承表示能用别人的什么东西xing

![](./../image/java/%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6.png)

## Override

注释@Override，检测函数对不对

方法重写，右键，generate，选择函数

## 访问同名字变量

name方法

this.name子类

super.name父类

## 默认的构造器

子类的无参和有参构造器，都默认先调用父类的无参构造器

子类默认第一句是super()代码

父类没有无参构造器，要自己给super传参数，例如super(a,b),给父类的有参构造器传参数