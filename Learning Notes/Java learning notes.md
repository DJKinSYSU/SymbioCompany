# 学习笔记
1. 面向对象的特征分为：抽象，继承，封装，多态性。

   抽象是把对象的特征和行为等提取出来构造类；

   继承是从一个类继承信息创建一个新类；

   封装是只能通过指定的接口访问封装在类中的数据和对数据进行操作；

   多态性就是用同样的对象引用调用同样的方法但是做了不同的事情。方法重载（overload）实现编译时的多态性（也称为前绑定），而方法重写（override）实现运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1). 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2). 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

2. 访问修饰符的区别
   ![img1](assets/markdown-img-paste-20190305181833159.png)
   类的成员不写访问修饰时默认为default。默认对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private）。受保护（protected）对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。Java中，外部类的修饰符只能是public或默认，类的成员（包括内部类）的修饰符可以是以上四种。

3. 数据类型

   Java中的基本数据类型只有8个：byte、short、int、long、float、double、char、boolean；除了基本类型（primitive type），剩下的都是引用类型（reference type），Java 5以后引入的枚举类型也算是一种比较特殊的引用类型。

4. goto和const都是Java中的保留字，在目前版本的Java中没有使用。

5. 因为s1+= 1;相当于s1 = (含数据类型)(s1 + 1);其中有隐含的强制类型转换。

6. int和Integer的区别：通过自动装箱/拆箱机制让原始类型与包装类型进行互相转换。比较Integer对象引用，==运算比较的不是值而是引用，一个Integer对象仅能代表-127-128之间的int值，超过的要分别用对象指代。

7. &运算符有两种用法：(1)按位与；(2)逻辑与。&&运算符是短路与运算，所以&&可以在左边为false时不判断右边的表达式。例如在验证用户登录时判定用户名不是null而且不是空字符串，应当写为：username != null &&!username.equals("")，二者的顺序不能交换，更不能用&运算符，因为第一个条件如果不成立，根本不能进行字符串的equals比较，否则会产生NullPointerException异常。注意：逻辑或运算符（|）和短路或运算符（||）的差别也是如此。

8. 内存中的栈(stack)、堆(heap)和方法区(method area)的用法：定义一个基本数据类型的变量，一个对象的引用，函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，堆是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured；方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量（literal）如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分。栈空间操作起来最快但是栈很小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈空间用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError。

  `String str = new String("hello");`

  上面的语句中变量str放在栈上，用new创建出来的字符串对象放在堆上，而"hello"这个字面量是放在方法区的。

9. Math.round(11.5)的返回值是12，Math.round(-11.5)的返回值是-11。四舍五入的原理是在参数上加0.5然后进行下取整。

10. 3.4是双精度数，将双精度型（double）赋值给浮点型（float）属于下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f =(float)3.4; 或者写成float f =3.4F;。

11. switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？在Java 5以前只能作用在byte、short、char、int上，在

12. 用最有效率的方法计算2乘以8？2 << 3（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。31 * num 等价于(num << 5) - num，左移5位相当于乘以2的5次方再减去自身就相当于乘以31，来产生哈希码（散列码）
  ```
  @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + areaCode;
        result = prime * result
                + ((lineNumber == null) ? 0 : lineNumber.hashCode());
        result = prime * result + ((prefix == null) ? 0 : prefix.hashCode());
        return result;
    }
  ```

13. 数组没有length()方法，有length 的属性。String 有length()方法。JavaScript中，获得字符串的长度是通过length属性得到的，这一点容易和Java混淆。

14. 在Java中，如何跳出当前的多重嵌套循环？ 在最外层循环前加一个标记如A，然后用break A;可以跳出多重循环。

15. 构造器（constructor）是否可被重写（override）？ 构造器不能被继承，因此不能被重写，但可以被重载。

16. 如果两个对象x和y满足x.equals(y) == true，它们的哈希码（hash code）应当相同。Java对于eqauls方法和hashCode方法是这样规定的：(1)如果两个对象相同（equals方法返回true），那么它们的hashCode值一定要相同；(2)如果两个对象的hashCode相同，它们并不一定相同。
>首先equals方法必须满足自反性（x.equals(x)必须返回true）、对称性（x.equals(y)返回true时，y.equals(x)也必须返回true）、传递性（x.equals(y)和y.equals(z)都返回true时，x.equals(z)也必须返回true）和一致性（当x和y引用的对象信息没有被修改时，多次调用x.equals(y)应该得到同样的返回值），而且对于任何非null值的引用x，x.equals(null)必须返回false。  
实现高质量的equals方法的诀窍包括：1. 使用==操作符检查"参数是否为这个对象的引用"；2. 使用instanceof操作符检查"参数是否为正确的类型"；3. 对于类中的关键属性，检查参数传入对象的属性是否与之相匹配；4. 编写完equals方法后，问自己它是否满足对称性、传递性、一致性；5. 重写equals时总是要重写hashCode；6. 不要将equals方法参数中的Object对象替换为其他的类型，在重写时不要忘掉@Override注解。

17. String 类是final类，不可以被继承。对String类型最好的重用方式是关联关系（Has-A）和依赖关系（Use-A）而不是继承关系（Is-A）。
