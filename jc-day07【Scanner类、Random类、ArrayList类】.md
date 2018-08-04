# day07【Scanner类、Random类、ArrayList类】

## 今日内容

*  API概述
*  Scanner类


*  Random类


*  ArrayList类


## 教学目标

- [ ] 能够明确API的使用步骤
- [ ] 能够使用Scanner类获得键盘录入数据
- [ ] 能够使用Random类生成随机数
- [ ] 能够使用数组存储自定义类型并遍历
- [ ] 能够使用ArrayList集合的构造方法创建ArrayList集合对象
- [ ] 能够使用ArrayList集合存储数据
- [ ] 能够使用ArrayList集合中常用的方法
- [ ] 能够使用ArrayList集合存储字符串并遍历
- [ ] 能够使用ArrayList集合存储自定义对象并遍历
- [ ] 能够使用ArrayList类作为形式参数和返回值类型

# 第1章 API

## 概述

**API(Application Programming Interface)，应用程序编程接口**。Java API是一本程序员的`字典` ，是JDK中提供**给我们使用的类的文档说明书**。

**注意!!!**这些类将底层的代码实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可。所以我们可以通过查询API的方式，来学习Java提供的类，并得知如何使用它们。

## API使用步骤

1. 打开帮助文档。
2. 点击显示，找到索引，看到输入框。
3. 你要找谁？在输入框里输入，然后回车。
4. 看包。java.lang下的类不需要导包，其他需要。
5. 看类的解释和说明。
6. 学习构造方法。
7. 使用成员方法。

# 第2章 Scanner类

了解了API的使用方式，我们通过Scanner类，熟悉一下查询API，并使用类的步骤。

## 2.1 什么是Scanner类

一个可以解析基本数据类型和字符串的简单文本扫描器。
例如，以下代码使用户能够从 System.in (系统输入,即键盘录入)中读取一个数： 

```java
Scanner sc = new Scanner(System.in);
int i = sc.nextInt();
```

> 备注：System.in 系统输入指的是通过键盘录入数据。

## 2.2 引用类型使用步骤

### 导包

使用import关键字导包，在类的所有代码之前导包，引入要使用的类型，java.lang包下的所有类无需导入。
格式：

```java
import 包名.类名;
```

举例：

```java
java.util.Scanner;
```

### 创建对象

使用该类的构造方法，创建一个该类的对象。
格式：

```java
数据类型  变量名  =  new 数据类型(参数列表);
```

举例：

```java
Scanner sc = new Scanner(System.in);
```

### 调用方法

调用该类的成员方法，完成指定功能。
格式：

```java  
变量名.方法名();
```

举例：

```java
int i = sc.nextInt(); // 接收一个键盘录入的整数
```

## 2.3	Scanner使用步骤

**查看类**

* `java.util.Scanner` ：该类需要import导入后使用。 

**查看构造方法**

* `public Scanner(InputStream source)` : 构造一个新的 `Scanner`，它生成的值是从指定的输入流扫描的。

**查看成员方法**

* ` public int nextInt() `：将输入信息的下一个标记扫描为一个 `int` 值。

使用Scanner类，完成接收键盘录入数据的操作，代码如下：

```java
//1. 导包
import java.util.Scanner;
public class Demo01_Scanner {
  	public static void main(String[] args) {
    	//2. 创建键盘录入数据的对象
    	Scanner sc = new Scanner(System.in);

    	//3. 接收数据
    	System.out.println("请录入一个整数：");
    	int i = sc.nextInt();

    	//4. 输出数据
    	System.out.println("i:"+i);
  	}
}
//---------------------------课堂演示代码--------------------------------------------------------
import java.util.Scanner;
public class Test01 {
    public static void main(String[] args) {
        //Scanner,sc
        Scanner sc = new Scanner(System.in);//f2,扫描,系统输入,键盘录入,sc对象名
        //温馨提示
        System.out.println("请输入一个整数");
        int i = sc.nextInt();//.var生成一个变量接收方法的返回值结果,enter键,输入完毕,接收整数
//        String i = sc.nextLine();//enter键,输入完毕,接收字符串
        System.out.println(i);//
    }
}
```



## 2.4	练习

### 求和

键盘录入两个数据并求和，代码如下：

```java
import java.util.Scanner;
public class Test01Scanner {
    public static void main(String[] args) {
        // 创建对象
        Scanner sc = new Scanner(System.in);
        // 接收数据
        System.out.println("请输入第一个数据：");
        int a = sc.nextInt();
        System.out.println("请输入第二个数据：");
        int b = sc.nextInt();
        // 对数据进行求和
        int sum = a + b;
        System.out.println("sum:" + sum);
    }
}
```

### 取最值

键盘录入三个数据并获取最大值，代码如下：

```java
import java.util.Scanner;
public class Test02Scanner {
    public static void main(String[] args) {
        // 创建对象
        Scanner sc = new Scanner(System.in);
        // 接收数据
        System.out.println("请输入第一个数据：");
        int a = sc.nextInt();
        System.out.println("请输入第二个数据：");
        int b = sc.nextInt();
        System.out.println("请输入第三个数据：");
        int c = sc.nextInt();

        // 如何获取三个数据的最大值
        int temp = (a > b ? a : b);
        int max = (temp > c ? temp : c);

        System.out.println("max:" + max);
    }
}
```

## 2.5 匿名对象【了解】

### 概念

创建对象时，只有创建对象的语句，却没有把对象地址值赋值给某个变量。虽然是创建对象的简化写法，但是应用场景非常有限。// new Scanner(System.in);

* **匿名对象** ：没有变量名(名字)的对象。

格式：

```java
new 类名(参数列表)；
```

举例：

```java
new Scanner(System.in)；
```

### 应用场景

1. 创建匿名对象直接调用方法，没有变量名。

```java
new Scanner(System.in).nextInt();  
```

2. 一旦调用两次方法，就是创建了两个对象，造成浪费，请看如下代码。

```java
new Scanner(System.in).nextInt();//new,新建的意思,每new一次就创建新的对象,开辟新的内存空间,浪费内存
new Scanner(System.in).nextInt();
```

> 小贴士：一个匿名对象，只能使用一次。

3. 匿名对象可以作为方法的参数和返回值

* 作为参数：

```java
class Test {
    public static void main(String[] args) {
     	// 普通方式
        Scanner sc = new Scanner(System.in);  
        input(sc);
      
        //匿名对象作为方法接收的参数
        input(new Scanner(System.in));
    }
  
 	public static void input(Scanner sc){//sc = new Scanner(System.in);
    	System.out.println(sc);
  	}
} 

```

* 作为返回值

```java
class Test2 {
  	public static void main(String[] args) {
     	// 普通方式
        Scanner sc = getScanner(); 
    }
    
  	public static Scanner getScanner(){
        //普通方式
        //Scanner sc = new Scanner(System.in);  
        //return sc;
      
        //匿名对象作为方法返回值
        return new Scanner(System.in);
	}
}
```



# 第3章 Random类

## 3.1 什么是Random类,随机数类,产生随机数

此类的实例用于生成伪随机数。

例如，以下代码使用户能够得到一个随机数：

```java
Random r = new Random();
int i = r.nextInt();//产生一个随机整数,有负数等
```

## 3.2 Random使用步骤

**查看类**

- `java.util.Random` ：该类需要 import导入使后使用。 

**查看构造方法**

- `public Random()`：创建一个新的随机数生成器。

**查看成员方法**

- ` public int nextInt(int n) `：返回一个伪随机数，范围在 `0` （包括）和`指定值 n` （不包括）之间的 `int` 值。

使用Random类，完成生成3个10以内的随机整数的操作，代码如下：

```java
//1. 导包
import java.util.Random;
public class Demo01_Random {
  	public static void main(String[] args) {
        //2. 创建键盘录入数据的对象
        Random r = new Random();

        for(int i = 0; i < 3; i++){
            //3. 随机生成一个数据
            int number = r.nextInt(10);
            //4. 输出数据
            System.out.println("number:"+ number);
        }		
    }
}

//-------------------------------------------课堂练习-------------------------------------------
//Random,随机数类,创建对象名.方法
Random r = new Random();//r
int i = r.nextInt(3);//3一定范围的数据数包含0到2,0-2,0,1,2,随机
System.out.println(i);
```

> 备注：创建一个`Random`对象，每次调用`nextInt()`方法，都会生成一个随机数。

## 3.3 练习

### 获取随机数

获取1-n之间的随机数，包含n，代码如下：

```java
// 导包
import java.util.Random;
public class Test01Random {
    public static void main(String[] args) {
        int n = 50; 
        // 创建对象
        Random r = new Random();
        // 获取随机数
        int number = r.nextInt(n) + 1;//0-49
        // 输出随机数
        System.out.println("number:" + number);
    }
}
```

### 猜数字小游戏	

游戏开始时，会随机生成一个1-100之间的整数`number` 。玩家猜测一个数字`guessNumber` ，会与`number` 作比较，系统提示大了或者小了，直到玩家猜中，游戏结束。  

> 小贴士：先运行程序代码，理解此题需求，经过分析后，再编写代码

```java
// 导包
import java.util.Random;
public class Test02Random {
    public static void main(String[] args) {
        // 系统产生一个随机数1-100之间的。
        Random r = new Random();
        int number = r.nextInt(100) + 1;
        while(true){
            // 键盘录入我们要猜的数据
            Scanner sc = new Scanner(System.in);//这句代码,放循环外面就不用不断创建对象更省内存
            System.out.println("请输入你要猜的数字(1-100)：");
            int guessNumber = sc.nextInt();

            // 比较这两个数据(用if语句)
            if (guessNumber > number) {
                System.out.println("你猜的数据" + guessNumber + "大了");
            } else if (guessNumber < number) {
                System.out.println("你猜的数据" + guessNumber + "小了");
            } else {
                System.out.println("恭喜你,猜中了");
                break;
            }
        }
    }
}
```



#  第4章 ArrayList类

## 4.1 引入——对象数组

使用学生数组，存储三个学生对象，代码如下：

```java
class Student {//我写在跟测试类同一个文件里面所以去掉了public
    private String name;
    private int age;
    
    //下面这一波代码都可以通过idea的快捷键alt insert自动生成
    public Student() {
    }
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    publicvoid setName(String name) {
        this.name = name;
    }
    publicint getAge() {
        return age;
    }
    publicvoid setAge(int age) {
        this.age = age;
    }
}

public class Test01StudentArray {
    public static void main(String[] args) {
        //创建学生数组
        Student[] students = new Student[3];//Student类,类型,引用数据类型都是null3固定死了

        //创建学生对象
        Student s1 = new Student("曹操",40);
        Student s2 = new Student("刘备",35);
        Student s3 = new Student("孙权",30);

        //把学生对象作为元素赋值给学生数组
        students[0] = s1;
        students[1] = s2;
        students[2] = s3;

        //遍历学生数组
        for(int x=0; x<students.length; x++) {//x索引
            Student s = students[x];//s = new Student("曹操",40);
            System.out.println(s.getName()+"---"+s.getAge());
        }
    }
}
```

到目前为止，我们想**存储对象数据**，**选择的容器，只有对象数组。而数组的长度是固定的，无法适应数据变化的需求**。为了解决这个问题，Java提供了另一个容器`java.util.ArrayList`  集合类,让我们可以更便捷的存储和操作对象数据。 

## 4.2 什么是ArrayList类,容器

`java.util.ArrayList` 是大小**可变的数组**的实现，存储在内的数据称为元素。此类提供一些方法来操作内部存储的元素。 `ArrayList` 中可不断添加元素，其大小也自动增长,所以**是个可以自动增长的容器,叫集合**,相当于气球!!!

## 4.3 ArrayList使用步骤

**查看类**

- `java.util.ArrayList <E>` ：该类需要 import导入使后使用。  

`<E>` ，表示一种指定的数据类型，叫做泛型(就业班学)。`E` ，取自Element（元素）的首字母。在出现`E` 的地方，我们使用一种**引用数据类型**将其替换即可，表示我们将存储哪种引用类型的元素。代码如下：

```java
ArrayList<String>，ArrayList<Student>
```

**查看构造方法**

- `public ArrayList() `：构造一个内容为空的集合,容器

基本格式:

```java 
ArrayList<String> list = new ArrayList<String>();
```

在JDK 7后,右侧泛型的尖括号之内可以留空，这叫可推导可省略原则(后面就业班学习lambda表达式也有这个原则)简化格式：

```java
ArrayList<String> list = new ArrayList<>();
```

**查看成员方法**

- ` public boolean add(E e)  `： 将指定的元素添加到此集合的尾部。

  参数 `E e `，在构造ArrayList对象时，`<E>`指定了什么数据类型，那么`add(E e)`方法中，只能添加什么数据类型的对象。

使用ArrayList类，存储三个字符串元素，代码如下：

```java
public class Test02StudentArrayList {
    public static void main(String[] args) {
        //创建集合对象调用add方法添加元素
        ArrayList<String> list = new ArrayList<>();
        System.out.println(list);//[]

        //添加元素
        String s1 = "曹操";
        String s2 = "刘备";
        String s3 = "孙权";

        list.add(s1);
        list.add(s2);
        list.add(s3);

     //打印集合,即打印集合对象名,默认会调用toString()方法,输出指定格式比如带有[],多个元素以逗号空格隔开
        System.out.println(list);//[曹操, 刘备, 孙权]
    }
    
}
```

## 4.4 常用方法和遍历

对于元素的操作,基本体现在——增、删、改、查。常用的方法有：

* `public boolean add(E e)`：将指定的元素添加到此集合的尾部//增


* `public E remove(int index)` ：移除此集合中指定位置上的元素。返回被删除的元素//删 

* `public E set(int index, E element)` ：设置集合指定位置的元素为后面传入的元素//改


* ` public E get(int index)` ：返回此集合中指定位置上的元素。返回获取的元素//查


* `public int size()` ：返回此集合中的元素个数。遍历集合时，可以控制索引范围，防止越界

这些都是最基本的方法，操作非常简单，代码如下:

```java
public class Demo01ArrayListMethod {
    public static void main(String[] args) {
        //创建集合对象
        ArrayList<String> list = new ArrayList<String>();

        //添加元素
        list.add("hello");
        list.add("world");
        list.add("java");

        //public E get(int index):返回指定索引处的元素
        System.out.println(list.get(0));//hello
        System.out.println(list.get(1));//world
        System.out.println(list.get(2));//java

        //public int size():返回集合中的元素的个数
        System.out.println(list.size());//3

        //public E remove(int index):删除指定索引处的元素，返回被删除的元素
        System.out.println(list.remove(0));//hello

        //public E set(int index, E element)：设置集合指定位置的元素为后面传入的元素
        list.set(0,"666");

        //遍历输出,得到集合里面的每一个元素
        for(int i = 0; i < list.size(); i++){
            System.out.println(list.get(i));//666换行输出java
        }
    }
}
```

## 4.5 如何存储基本数据类型

ArrayList对象不能存储基本类型，只能存储引用类型的数据。类似**`<int>`不能写**，但是存储基本数据类型对应的包装类(引用数据类型)型是可以的。所以，想要存储基本类型数据，`<>`中的数据类型，必须转换后才能编写，转换写法如下：

| 基本类型 | 基本类型对应的包装类 |
| -------- | -------------------- |
| byte     | Byte                 |
| short    | Short                |
| **int**  | **Integer**          |
| long     | Long                 |
| double   | Double               |
| float    | Float                |
| **char** | **Character**        |
| boolean  | Boolean              |

我们发现，只有`Integer`和`Character`需要特殊记忆，其他基本类型只是首字母大写即可。那么存储基本类型数据，代码如下：

```java
public class Demo02ArrayListMethod {
	public static void main(String[] args) {
    	ArrayList<Integer> list = new ArrayList<Integer>();//<不能写int>
    	list.add(1);//int和Integer可以互相转换
    	list.add(2);//存的都是对象
    	list.add(3);
    	list.add(4);

    	System.out.println(list);//[1, 2, 3, 4]     
  	}
}
```

## 4.6 ArrayList练习

### 数值添加到集合

生成6个1~33之间的随机整数,添加到集合,并遍历 

```java
public class Test01ArrayList {
    public static void main(String[] args) {
        // 创建ArrayList 对象
        ArrayList<Integer> list = new ArrayList<>();

        // 添加随机数到集合
        // 创建Random 对象
        Random random = new Random();

        for (int i = 0; i < 6; i++) {
            int r = random.nextInt(33) + 1;
            list.add(r);
        }

        // 遍历集合输出,list.for
        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}
```

### 对象添加到集合

自定义4个学生对象,添加到集合,并遍历

```java
public class Test02ArrayList {
    public static void main(String[] args) {
        //创建集合对象
        ArrayList<Student> list = new ArrayList<Student>();

        //创建学生对象
        Student s1 = new Student("赵丽颖",18);
        Student s2 = new Student("唐嫣",20);
        Student s3 = new Student("景甜",25);
        Student s4 = new Student("柳岩",19);

        //把学生对象作为元素添加到集合中
        list.add(s1);
        list.add(s2);
        list.add(s3);
        list.add(s4);

        //遍历集合
        for(int x = 0; x < list.size(); x++) {
            Student s = list.get(x);
            System.out.println(s.getName()+"---"+s.getAge());
        }
    }
}
```

### 打印集合方法

定义以指定格式打印集合的方法(ArrayList类型作为参数)，使用{}扩起集合，使用@分隔每个元素。输出格式参照 {元素@元素@元素}。

```java
public class Test03ArrayList {
    public static void main(String[] args) {
        // 创建集合对象
        ArrayList<String> list = new ArrayList<String>();

        // 添加字符串到集合中
        list.add("张三丰");
        list.add("宋远桥");
        list.add("张无忌");
        list.add("殷梨亭");

        // 调用方法
        printArrayList(list);//{张三丰@宋远桥@张无忌@殷梨亭}//
    }

    public static void printArrayList(ArrayList<String> list) {
        // 拼接左括号
        System.out.print("{");

        // 遍历集合
        for (int i = 0; i < list.size(); i++) {
            // 获取元素
            String s = list.get(i);
            // 拼接@符号
            if (i != list.size() - 1) {
                System.out.print(s + "@");
            } else {
                // 最后一个元素,拼接右括号
                System.out.print(s + "}");
            }
        }

    }
}
```

### 获取集合方法

定义获取偶数元素集合的方法(ArrayList类型作为返回值)

```java
public class Test04ArrayList {
    public static void main(String[] args) {
        // 创建ArrayList 对象
        ArrayList<Integer> list = new ArrayList<>();

        // 添加随机数到集合
        // 创建Random 对象
        Random random = new Random();
        for (int i = 0; i < 20; i++) {
            int r = random.nextInt(1000) + 1;
            list.add(r);//都是奇数
        }

        // 调用偶数集合的方法
        ArrayList<Integer> arrayList = getArrayList(list);
        System.out.println(arrayList);
    }

    public static ArrayList<Integer> getArrayList(ArrayList<Integer> list) {
        // 创建小集合,来保存偶数
        ArrayList<Integer> smallList = new ArrayList<>();

        // 遍历list
        for (int i = 0; i < list.size(); i++) {
            // 获取元素
            Integer num = list.get(i);
            // 判断为偶数,添加到小集合中
            if (num % 2 == 0){
                smallList.add(num);
            }
        }

        // 返回小集合
        return smallList;
    }
    
}
```



## 4.7 扩展,普通for循环遍历的过程中删除元素两种方案

~~~java
import java.util.ArrayList;
public class Test13 {
    public static void main(String[] args) {
        //遍历过程中删除元素,注意事项
        ArrayList<String> al = new ArrayList();
        al.add("a");
        al.add("b");//1//b
        al.add("b");//2//c
        al.add("c");

//        System.out.println(al);
//        //遍历过程中,如果得到元素是b的时候,全部删除
//        for (int i = 0; i < al.size(); i++) {//
//            String s = al.get(i);//s代表每一个元素,字符串内容值是否相等equals方法,相等返回true
//            if ("b".equals(s)){
//                al.remove(i);//b,删完元素,把索引回退一下
//                i--;//i=i-1;
//            }
//        }
        
        //从后往前删,反向遍历
        for (int i = al.size() - 1; i >= 0; i--) {//最大索引到0
            String s = al.get(i);

            if ("b".equals(s)){
                al.remove(i);
            }
        }

        //遍历
        for (int i = 0; i < al.size(); i++) {
            System.out.println(al.get(i));
        }
    }
}
~~~

