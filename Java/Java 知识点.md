###### 修饰符/访问权限static

下面哪个修饰符修饰的变量是所有同一个类生成的对象所共享的？

A public

B private

C static

D final

正确答案：C

static 修饰某个字段时，肯定会改变字段创建的方式（每个被 static 修饰的字段对于每个类来说只有一份存储空间，而非 static 修饰的字段对于每一个对象来说都有一个存储空间）。

static 可以理解为类层面的变量，对象共同拥有，可以通过`类名.变量名`操作，也可以通过`对象名.变量名`操作。

对于 private，是一种访问权限，static 是共享。共享相当于公共财产，被所有人拥有；访问权限相当于公交车，你可以坐，但是它不属于每一个的财产。

当某一个对象修改了 stati 变量，其他对象访问时得到的就是修改后的值，这叫共享。



###### 构造方法

判断题：用户不能调用构造方法，只能通过 new 关键字自动调用。

答案：错误

1 在构造方法中，可以通过 this.构造方法名字() 调用其他构造方法；

2 在子类中，用户可以通过 super() 调用父类中指定的构造方法；

3 反射机制对于任意一个类，都能够知道这个类的所有属性和方法，包括类的构造方法。

`class.forName(类名).newInstance();`

`Constructor constructor = 类名.class.getConstructor();`

`类 obj = constructor.newInstance();` 

###### final

final 类型变量必须初始化，不可更改。

初始化的方式：

1 定义时初始化；

2 final 变量可以在初始化块中初始化，但是不可在静态初始块中初始化，只能是静态的 final 成员变量才能在静态初始化块中初始化；

3 在类的构造器中初始化，但是静态 final 成员变量是不能在构造函数初始化的。（因为静态变量比构造函数先执行）

```
class Foo{

	final int j;
	int i;

	public void doSomething(){

		System.out.println(++j+i);
	}
}
```

的输出是？

A 0 B 1 C 2 D 不能执行，因为编译有错误

答案：D

###### Thread/异常

Thread.sleep() 是否会抛出 checked exception？ 答案：会

题目意思指是否会抛出一个需要检查的异常，并不是异常名字叫 checked exception。

Thread.sleep() 会抛出 InterruptedException，该异常属于 checked exception，也就是编译时异常。必须显式的捕获异常，而不能继续往外层抛，此异常需要该线程自己来解决。

checked exception，编译时异常，用 try..catch 处理，或 throw 处理；

runtime exception，运行时异常，本函数体不必须处理。比如 IIlegalArgumentException。

###### Java / C++

JDK 中提供的 java、javac、jar 等开发工具也是用 Java 编写的。答案：对

据目前资料，JVM 是 C++ 实现的。其他都是 Java。

和操作系统打交道的 Java 实现不了。

###### 多态

类多态的向上转型：父类只能调用父类方法或者子类覆盖后的方法，而子类中的单独方法则是无法调用的。

关于子类继承父类中方法的调用，只要不是用 super 调用，调用的都是子类中覆写父类的方法。

假定 Base b = new Derived(); 调用执行 b.methodOne() 后，输出结果是什么？

```java
public class Base{
  public void methodOne(){
    System.out.print("A");
    methodTwo();
  }
  
  public void methodTwo(){
    System.out.print("B");
  }
}

public class Derived extends Base{
  public void methodOne(){
    super();
    system.out.print("C");
  }
  
  public void methodTwo(){
    super.methodTwo();
    System.out.print("D");
  }
}
```

答案：ABDC