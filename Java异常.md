### Java异常
一，异常的概述

1.分为：编译时异常和运行时异常

```
编译时异常：一般是指语法错误，比较容易修正。
运行时异常：运行错误和逻辑错误
异常事件：异常的类创建对象出现错误
```


2.异常的处理机制：
   

```
    异常处理机制能让程序在异常发生时，按照代码的预先设定的异常处理逻辑，针对性地处理异常，让程序尽最大可能恢复正常并继续执行，且保持代码的清晰。
      Java中的异常可以是函数中的语句执行时引发的，也可以是程序员通过throw 语句手动抛出的，只要在Java程序中产生了异常，就会用一个对应类型的异常对象来封装异常，JRE就会试图寻找异常处理程序来处理异常。

Throwable类是Java异常类型的顶层父类，一个对象只有是 Throwable 类的（直接或者间接）实例，他才是一个异常对象，才能被异常处理机制识别。JDK中内建了一些常用的异常类，我们也可以自定义异常。
```


3.Java异常的分类和类结构图

```
Throwable又派生出Error类和Exception类。

错误：Error类以及他的子类的实例，代表了JVM本身的错误。错误不能被程序员通过代码处理，Error很少出现。因此，程序员应该关注Exception为父类的分支下的各种异常类。

异常：Exception以及他的子类，代表程序运行时发送的各种不期望发生的事件。可以被Java异常处理机制使用，是异常处理的核心。
```


> 总体上我们根据Javac对异常的处理要求，将异常类分为2类。

```
非检查异常（unckecked exception）：Error 和 RuntimeException 以及他们的子类。javac在编译时，不会提示和发现这样的异常，不要求在程序处理这些异常。所以如果愿意，我们可以编写代码处理（使用try…catch…finally）这样的异常，也可以不处理。对于这些异常，我们应该修正代码，而不是去通过异常处理器处理 。这样的异常发生的原因多半是代码写的有问题。如除0错误ArithmeticException，错误的强制类型转换错误ClassCastException，数组索引越界ArrayIndexOutOfBoundsException，使用了空对象NullPointerException等等。

检查异常（checked exception）：除了Error 和 RuntimeException的其它异常。javac强制要求程序员为这样的异常做预备处理工作（使用try…catch…finally或者throws）。在方法中要么用try-catch语句捕获它并处理，要么用throws子句声明抛出它，否则编译不会通过。这样的异常一般是由程序的运行环境导致的。因为程序可能被运行在各种未知的环境下，而程序员无法干预用户如何使用他编写的程序，于是程序员就应该为这样的异常时刻准备着。如SQLException , IOException,ClassNotFoundException 等。

需要明确的是：检查和非检查是对于javac来说的，这样就很好理解和区分了。
```

 

```
throw 异常抛出语句
throw exceptionObject

程序员也可以通过throw语句手动显式的抛出一个异常。throw语句的后面必须是一个异常对象。

throw 语句必须写在函数中，执行throw 语句的地方就是一个异常抛出点，它和由JRE自动形成的异常抛出点没有任何差别。
```

 

 

```
throws 函数声明
      throws声明：如果一个方法内部的代码会抛出检查异常（checked exception），而方法自己又没有完全处理掉，则javac保证你必须在方法的签名上使用throws关键字声明这些可能抛出的异常，否则编译不通过。

    throws是另一种处理异常的方式，它不同于try…catch…finally，throws仅仅是将函数中可能出现的异常向调用者声明，而自己则不具体处理。

      采取这种异常处理的原因可能是：方法本身不知道如何处理这样的异常，或者说让调用者处理更好，调用者需要为可能发生的异常负责。

 
注意：抛出会抛出多个异常，并不是处理异常，而上抛到上一级，谁调用谁处理。多个异常之间用逗号隔开（扔是一种消极处理异常的方式，如果在要出现异常的地方，用new Exception（）;如果能处理的完这个异常，则不用在该区域的外面写throws了，如果处理不了必须要在外面写上这个throws抛出的异常，来声明未处理完的异常。
```

```
package exception;
 
import java.util.Scanner;
public class TestException2 {
	public static void main(String[] args) {
		System.out.println("请输入A和B的值");
	    calculter();
	}
	public static void calculter() {
		double   num = 0,num1=0,num2=0;
		Scanner scanner=new Scanner(System.in);
		num1=scanner.nextInt();
	    num2=scanner.nextInt();
		num=num1/num2;
		System.out.println("结果为："+num);
		scanner.close();
	}
}
```

> 上面的num2如果是0，则会抛出ArithmeticException的异常，那么我们在num2的区域加上处理异常的代码

```
第一种：throw new ArithmeticException（）；
package exception;
 
import java.util.Scanner;
public class ThrowExceotion {
	public static void main(String[] args) {
		System.out.println("请输入A和B的值");
	    calculter();
	}
	public static void calculter() {
		double   num = 0,num1=0,num2=0;
		Scanner scanner=new Scanner(System.in);
		num1=scanner.nextInt();
	    num2=scanner.nextInt();
	    if(num2==0) {
	    	throw new ArithmeticException("除数为0！");
	    }
		num=num1/num2;
		System.out.println("结果为："+num);
		scanner.close();
	}
}
```

> 1.当我输入的num2为0的时候，运行结果如下图


```
2.throw和throws同时存在的情况
package exception;
 
import java.util.Scanner;
public class ThrowExceotion {
	public static void main(String[] args) {
		System.out.println("请输入A和B的值");
	    calculter();
	}
	public static void calculter() throws ArithmeticException{
		double   num = 0,num1=0,num2=0;
		Scanner scanner=new Scanner(System.in);
		num1=scanner.nextInt();
	    num2=scanner.nextInt();
	    if(num2==0) {
	    	throw new ArithmeticException("除数为0！");
	    }
		num=num1/num2;
		System.out.println("结果为："+num);
		scanner.close();
	}
}
```



>总结：我们发现当我们知道某个地方会发生异常的情况，我们用throw new ArithmeticException();手动捕获异常。这样可以对异常进行处理。这种情况可以对异常进行处理，但是有的时候，手动触发的异常也不一定能处理所碰到的异常，所以我们在throw的基础之上在在该异常区域的外面再throws这个异常，使其抛给调用他的区域，让他们再去处理这个异常。所以这样的写法保证了异常能报尽可能的都处理。
 

第三种;try-catch-finally

```
package exception;
import java.util.Scanner;
public class TestException {
	public static void main(String[] args) {
		System.out.println("请输入A和B的值");
	    calculter();
	}
	public static void calculter() {
		double   num = 0,num1=0,num2=0;
		Scanner scanner=new Scanner(System.in);
		try {	
		    num1=scanner.nextInt();
			num2=scanner.nextInt();
		}catch(ArithmeticException e) {
			e.printStackTrace();
		}finally {
		   System.out.println("除数不能为0！");
		}
			num=num1/num2;
		System.out.println("结果为："+num);
		scanner.close();
	}
}
```

但我输入的num2为0的时候的运行结果为：


 
注意：


（1）catch可以有多个，异常的捕获必须从小类的异常到大类的异常，最多执行一个捕捉语句块，抓执行的从第一个开始执行，所以一般前面放的都是子类，也就是抓执行的一般化，会逐步趋于一般化。如果前面出现异常，后面依然是可以执行的，但是如果的扔后面的语句就不不会再执行。
（2）最后：一定会执行的代码，一般用来做资源的释放
       

try…catch…finally语句块
 

try{
     //try块中放可能发生异常的代码。
     //如果执行完try且不发生异常，则接着去执行finally块和finally后面的代码（如果有的话）。
     //如果发生异常，则尝试去匹配catch块。
 
}catch(SQLException SQLexception){
    //每一个catch块用于捕获并处理一个特定的异常，或者这异常类型的子类。Java7中可以将多个异常声明在一个catch中。
    //catch后面的括号定义了异常类型和异常参数。如果异常与之匹配且是最先匹配到的，则虚拟机将使用这个catch块来处理异常。
    //在catch块中可以使用这个块的异常参数来获取异常的相关信息。异常参数是这个catch块中的局部变量，其它块不能访问。
    //如果当前try块中发生的异常在后续的所有catch中都没捕获到，则先去执行finally，然后到这个函数的外部caller中去匹配异常处理器。
    //如果try中没有发生异常，则所有的catch块将被忽略。
 
}catch(Exception exception){
    //...
}finally{
 
    //finally块通常是可选的。
   //无论异常是否发生，异常是否匹配被处理，finally都会执行。
   //一个try至少要有一个catch块，否则， 至少要有1个finally块。但是finally不是用来处理异常的，finally不会捕获异常。
  //finally主要做一些清理工作，如流的关闭，数据库连接的关闭等。 
}
需要注意的地方：
 

1、try块中的局部变量和catch块中的局部变量（包括异常变量），以及finally中的局部变量，他们之间不可共享使用。

2、每一个catch块用于处理一个异常。异常匹配是按照catch块的顺序从上往下寻找的，只有第一个匹配的catch会得到执行。匹配时，不仅运行精确匹配，也支持父类匹配，因此，如果同一个try块下的多个catch异常类型有父子关系，应该将子类异常放在前面，父类异常放在后面，这样保证每个catch块都有存在的意义。

3、java中，异常处理的任务就是将执行控制流从异常发生的地方转移到能够处理这种异常的地方去。也就是说：当一个函数的某条语句发生异常时，这条语句的后面的语句不会再执行，它失去了焦点。执行流跳转到最近的匹配的异常处理catch代码块去执行，异常被处理完后，执行流会接着在“处理了这个异常的catch代码块”后面接着执行。
有的编程语言当异常被处理后，控制流会恢复到异常抛出点接着执行，这种策略叫做：resumption model of exception handling（恢复式异常处理模式 ）
而Java则是让执行流恢复到处理了异常的catch块后接着执行，这种策略叫做：termination model of exception handling（终结式异常处理模式）

 

举例说明：

```
package exception;
public class TrycatchTest {
	public static void main(String[] args) {
        try {
        	test();
		} catch (ArithmeticException e) {	
			System.out.println("异常处理");
		}
	}
	public static void test() {
		int a=10/0;
		System.out.println(a);
		System.out.println("我会被执行吗？");
	}
 
}
```

运行结果为：



可以看出这个函数内的一个输出语句未被执行。说明当一个函数内发生异常是，函数内部异常后面的语句不会得到执行。

 

finally块
finally块不管异常是否发生，只要对应的try执行了，则它一定也执行。只有一种方法让finally块不执行：System.exit()。因此finally块通常用来做资源释放操作：关闭文件，关闭数据库连接等等。

良好的编程习惯是：在try块中打开资源，在finally块中清理释放这些资源。

需要注意的地方:

1、finally块没有处理异常的能力。处理异常的只能是catch块。

2、在同一try…catch…finally块中 ，如果try中抛出异常，且有匹配的catch块，则先执行catch块，再执行finally块。如果没有catch块匹配，则先执行finally，然后去外面的调用者中寻找合适的catch块。

3、在同一try…catch…finally块中 ，try发生异常，且匹配的catch块中处理异常时也抛出异常，那么后面的finally也会执行：首先执行finally块，然后去外围调用者中寻找合适的catch块。

但是也有特例！

异常的链化
在一些大型的，模块化的软件开发中，一旦一个地方发生异常，则如骨牌效应一样，将导致一连串的异常。假设B模块完成自己的逻辑需要调用A模块的方法，如果A模块发生异常，则B也将不能完成而发生异常，但是B在抛出异常时，会将A的异常信息掩盖掉，这将使得异常的根源信息丢失。异常的链化可以将多个模块的异常串联起来，使得异常信息不会丢失。

异常链化:以一个异常对象为参数构造新的异常对象。新的异对象将包含先前异常的信息。这项技术主要是异常类的一个带Throwable参数的函数来实现的。这个当做参数的异常，我们叫他根源异常（cause）。

查看Throwable类源码，可以发现里面有一个Throwable字段cause，就是它保存了构造时传递的根源异常参数。这种设计和链表的结点类设计如出一辙，因此形成链也是自然的了。

```
public class Throwable implements Serializable {
    private Throwable cause = this;
 
    public Throwable(String message, Throwable cause) {
        fillInStackTrace();
        detailMessage = message;
        this.cause = cause;
    }
     public Throwable(Throwable cause) {
        fillInStackTrace();
        detailMessage = (cause==null ? null : cause.toString());
        this.cause = cause;
    }
 
    //........
}
```

下面是一个例子，演示了异常的链化：从命令行输入2个int，将他们相加，输出。输入的数不是int，则导致getInputNumbers异常，从而导致add函数异常，则可以在add函数中抛出

一个链化的异常。

```
package exception;
 
import java.util.ArrayList;
import java.util.InputMismatchException;
import java.util.List;
import java.util.Scanner;
 
public class ThrowTest {
 
	public static void main(String[] args) {
		try {
			int sum=add();
			System.out.println(sum);
		}catch(Exception e) {
			e.printStackTrace();
		}
}
	@SuppressWarnings("deprecation")
	public static List<Integer>  getnumber() {
	   List<Integer>num=new ArrayList<>();
		Scanner intput =new Scanner(System.in);
		System.out.println("请输入两个数字：");
		try {
		int num1=intput.nextInt();
		int num2=intput.nextInt();
		num.add(new Integer(num1));
		num.add(new Integer(num2));
		}catch(InputMismatchException e) {
			System.out.println("类型错误");
		}finally {
			intput.close();
		}
		return num;
	}
	public static int  add() {
		int sum = 0;
		try {
		List<Integer> integers =getnumber();
	    sum =integers.get(0)+integers.get(1);
		}catch(InputMismatchException e) {
				System.out.println("计算失败");
		}
		return sum;
	}
	
}
```

在创建的一个ArrayList数组中，如果输入的不是数字，则会出现InputMissMatchException异常，然后在add函数中还会出现InputMissMatchException的异常。最后在main方法中。用Exception。



自定义异常
如果要自定义异常类，则扩展Exception类即可，因此这样的自定义异常都属于检查异常（checked exception）。如果要自定义非检查异常，则扩展自RuntimeException。

按照国际惯例，自定义的异常应该总是包含如下的构造函数：

一个无参构造函数
一个带有String参数的构造函数，并传递给父类的构造函数。
一个带有String参数和Throwable参数，并都传递给父类构造函数
一个带有Throwable 参数的构造函数，并传递给父类的构造函数。
下面是IOException类的完整源代码，可以借鉴。

 

```
public class IOException extends Exception
{
    static final long serialVersionUID = 7818375828146090155L;
 
    public IOException()
    {
        super();
    }
 
    public IOException(String message)
    {
        super(message);
    }
 
    public IOException(String message, Throwable cause)
    {
        super(message, cause);
    }
 
    public IOException(Throwable cause)
    {
        super(cause);
    }
}
```

异常的注意事项
1、当子类重写父类的带有 throws声明的函数时，其throws声明的异常必须在父类异常的可控范围内——用于处理父类的throws方法的异常处理器，必须也适用于子类的这个带throws方法 。这是为了支持多态。

例如，父类方法throws 的是2个异常，子类就不能throws 3个及以上的异常。父类throws IOException，子类就必须throws IOException或者IOException的子类。

2、Java程序可以是多线程的。每一个线程都是一个独立的执行流，独立的函数调用栈。如果程序只有一个线程，那么没有被任何代码处理的异常 会导致程序终止。如果是多线程的，那么没有被任何代码处理的异常仅仅会导致异常所在的线程结束。

也就是说，Java中的异常是线程独立的，线程的问题应该由线程自己来解决，而不要委托到外部，也不会直接影响到其它线程的执行。

finally块和return
首先一个不容易理解的事实：在 try块中即便有return，break，continue等改变执行流的语句，finally也会执行。

finally中的return 会覆盖 try 或者catch中的返回值。

```
package exception;
 
public class ReturnException {
 
	public static void main(String[] args)
    {
        int result
        result  =  foo();
        System.out.println(result);     //4
        result = bar();
        System.out.println(result);    //3
    }
    @SuppressWarnings("finally")
    public static int foo()
    {
        try{
            int a = 5 / 0;
        } catch (Exception e){
            return 1;
        } finally{
            return 4;
        }
    }
 
    @SuppressWarnings("finally")
    public static int bar()
    {
        try {
            return 1;
        }finally {
            return 3;
        }
    }
}
```

finally中的return会抑制（消灭）前面try或者catch块中的异常

```
package exception;
 
public class ReturnException {
 
	public static void main(String[] args)
    {
        int result;
        try{
            result = foo();
            System.out.println(result);           //输出100
        } catch (Exception e){
            System.out.println(e.getMessage());    //没有捕获到异常
        }
        try{
            result  = bar();
            System.out.println(result);           //输出100
        } catch (Exception e){
            System.out.println(e.getMessage());    //没有捕获到异常
        }
    }
    //catch中的异常被抑制
    @SuppressWarnings("finally")
    public static int foo() throws Exception
    {
        try {
            int a = 5/0;
            return 1;
        }catch(ArithmeticException amExp) {
            throw new Exception("我将被忽略，因为下面的finally中使用了return");
        }finally {
            return 100;
        }
    }
    //try中的异常被抑制
    @SuppressWarnings("finally")
    public static int bar() throws Exception
    {
        try {
            int a = 5/0;
            return 1;
        }finally {
            return 100;
        }
    }
}
```

finally中的异常会覆盖（消灭）前面try或者catch中的异常

```
package exception;
 
public class ReturnException {
	public static void main(String[] args)
    {
        int result;
        try{
            result = foo();
        } catch (Exception e){
            System.out.println(e.getMessage());    //输出：我是finaly中的Exception
        }
        try{
            result  = bar();
        } catch (Exception e){
            System.out.println(e.getMessage());    //输出：我是finaly中的Exception
        }
    }
    //catch中的异常被抑制
    @SuppressWarnings("finally")
    public static int foo() throws Exception
    {
        try {
            int a = 5/0;
            return 1;
        }catch(ArithmeticException amExp) {
            throw new Exception("我将被忽略，因为下面的finally中抛出了新的异常");
        }finally {
            throw new Exception("我是finaly中的Exception");
        }
    }
    //try中的异常被抑制
    @SuppressWarnings("finally")
    public static int bar() throws Exception
    {
        try {
            int a = 5/0;
            return 1;
        }finally {
            throw new Exception("我是finaly中的Exception");
        }
    }
}
```

#### 总结：
上面的3个例子都异于常人的编码思维，因此我建议：

不要在fianlly中使用return。
不要在finally中抛出异常。
减轻finally的任务，不要在finally中做一些其它的事情，finally块仅仅用来释放资源是最合适的。
将尽量将所有的return写在函数的最后面，而不是try … catch … finally中。
上面如果有错误，请指出！