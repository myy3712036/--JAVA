# day09【继承、super、this、抽象类】

## 今日内容

- 三大特性——继承
- 方法重写
- super关键字
- this关键字
- 抽象类

## 教学目标

- [ ] 能够解释类名作为参数和返回值类型
- [ ] 能够写出类的继承格式
- [ ] 能够说出继承的特点
- [ ] 能够说出子类调用父类的成员特点
- [ ] 能够说出方法重写的概念
- [ ] 能够说出super可以解决的问题
- [ ] 描述抽象方法的概念
- [ ] 写出抽象类的格式
- [ ] 写出抽象方法的格式
- [ ] 能够说出父类抽象方法的存在意义
- [ ] 能够完成发红包案例的代码逻辑

# 第一章 继承 

## 1.1 概述

## 今天概念性的内容较多,代码会写会用即可,部分概念有时间记忆

### 由来

多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要继承那一个类即可。如图所示：

![](img/1.jpg)

其中，多个类可以称为**子类**，单独那一个类称为**父类**、**超类（superclass）**或者**基类**。

继承描述的是事物之间的所属关系，这种关系是：`is-a` 的关系(谁是谁的一种)。例如，图中兔子属于食草动物，食草动物属于动物。可见，父类更通用，子类更具体。我们通过继承，可以使多种事物之间形成一种关系体系。

### 定义//记忆

* **继承**：就是子类继承父类的**属性**和**行为**，使得子类对象具有与父类相同的属性、相同的行为。子类可以直接访问父类中的**非私有**的属性(成员变量)和行为(成员方法)。

### 好处//记忆

1. 提高**代码的复用性**(少写了很多代码实现一样的功能)
2. 类与类之间产生了关系，是**多态的前提**

## 1.2 继承的格式

通过 `extends` 关键字，可以声明一个子类继承另外一个父类，定义格式如下：

```java
class 父类 {
	...
}

class 子类 extends 父类 {
	...
}

```

继承演示，代码如下：

```java
/*
 * 定义员工类Employee，做为父类
 */
class Employee {
	String name; // 定义name属性
	// 定义员工的工作方法
	public void work() {
		System.out.println("尽心尽力地工作");
	}
}

/*
 * 定义讲师类Teacher 继承 员工类Employee
 */
class Teacher extends Employee {
	// 定义一个打印name的方法
	public void printName() {
		System.out.println("name=" + name);
	}
}

/*
 * 定义测试类
 */
public class ExtendDemo01 {
	public static void main(String[] args) {
        // 创建一个讲师类对象
		Teacher t = new Teacher();
      
        // 为该员工类的name属性进行赋值
		t.name = "小明"; 
      
      	// 调用该员工的printName()方法
		t.printName(); // name = 小明
		
      	// 调用Teacher类继承来的work()方法
      	t.work();  // 尽心尽力地工作
	}
}
```

## 1.3 继承后的特点——成员变量,就近原则,子类有就使用子类的,否则使用父类的//记忆

当类之间产生了关系后，其中各类中的成员变量，又产生了哪些影响呢？

### 成员变量不重名

如果子类父类中出现**不重名**的成员变量，这时的访问是**没有影响的**。代码如下：

```java
class Fu {
	// Fu中的成员变量。
	int num = 5;
}

class Zi extends Fu {
	// Zi中的成员变量
	int num2 = 6;
	// Zi中的成员方法
	public void show() {
		// 访问父类中的num，
		System.out.println("Fu num="+num); // 继承而来，所以直接访问。
		// 访问子类中的num2
		System.out.println("Zi num2="+num2);
	}
}

class ExtendDemo02 {
	public static void main(String[] args) {
        // 创建子类对象
		Zi z = new Zi(); 
      	// 调用子类中的show方法
		z.show();  
	}
}
演示结果：
Fu num = 5
Zi num2 = 6
```

### 成员变量重名

如果子类父类中出现**重名**的成员变量，这时的访问是**有影响的**。代码如下：

```java
class Fu {
	// Fu中的成员变量。
	int num = 5;
}

class Zi extends Fu {
	// Zi中的成员变量
	int num = 6;
	public void show() {
		// 访问父类中的num
		System.out.println("Fu num=" + num);//就近原则,子类有就使用子类的,否则使用父类的
		// 访问子类中的num
		System.out.println("Zi num=" + num);
	}
}

class ExtendsDemo03 {
	public static void main(String[] args) {
      	// 创建子类对象
		Zi z = new Zi(); 
      	// 调用子类中的show方法
		z.show(); 
	}
}
演示结果：
Fu num = 6
Zi num = 6
```

子父类中出现了同名的成员变量时，在子类中需要访问父类中非私有成员变量时，需要使用`super` 关键字，修饰父类成员变量，类似于之前学过的 `this` 。

使用格式：

```java
super.父类成员变量名
```

子类方法需要修改，代码如下：

```java
class Zi extends Fu {
	// Zi中的成员变量
	int num = 6;
	public void show() {
		//访问父类中的num
		System.out.println("Fu num=" + super.num);
		//访问子类中的num
		System.out.println("Zi num=" + this.num);
	}
}
演示结果：
Fu num = 5
Zi num = 6
```

> 小贴士：Fu 类中的成员变量是非私有的，子类中可以直接访问。若Fu 类中的成员变量私有了，子类是不能直接访问的。通常编码时，我们遵循封装的原则，使用private修饰成员变量，那么如何访问父类的私有成员变量呢？对！可以在父类中提供公共的getXxx方法和setXxx方法。

## 1.4 继承后的特点——成员方法,就近原则,子类有就使用子类的,否则使用父类的//记忆

当类之间产生了关系，其中各类中的成员方法，又产生了哪些影响呢？

### 成员方法不重名

如果子类父类中出现**不重名**的成员方法，这时的调用是**没有影响的**。对象调用方法时，会先在子类中查找有没有对应的方法，若子类中存在就会执行子类中的方法，若子类中不存在就会执行父类中相应的方法。代码如下：

```java
class Fu{
	public void show(){
		System.out.println("Fu类中的show方法执行");
	}
}

class Zi extends Fu{
	public void show2(){
		System.out.println("Zi类中的show2方法执行");
	}
}

public  class ExtendsDemo04{
	public static void main(String[] args) {
		Zi z = new Zi();
     	//子类中没有show方法，但是可以找到父类方法去执行
		z.show(); 
		z.show2();
	}
}
```

### 成员方法重名——重写(Override)//记忆

如果子类父类中出现**重名**的成员方法，这时的访问是一种特殊情况，叫做**方法重写** (Override)。

* **方法重写** ：子类中出现与父类一模一样的方法时（返回值类型，方法名和参数列表都相同），会出现覆盖效果，也称为重写或者复写(**能够继承拿到然后在子类重写一遍)**//记忆

代码如下：

```java
class Fu {
	public void show() {
		System.out.println("Fu show");
	}
}

class Zi extends Fu {
	//子类重写了父类的show方法
	public void show() {
		System.out.println("Zi show");
	}
}

public class ExtendsDemo05{
	public static void main(String[] args) {
		Zi z = new Zi();
     	// 子类中有show方法，只执行重写后的show方法
		z.show();  // Zi show
	}
}
```

### 重写的应用//记忆

子类可以根据需要，定义特定于自己的行为。既沿袭了父类的功能名称，又根据子类的需要重新实现父类方法，从而进行扩展增强。比如新的手机增加来电显示头像的功能，代码如下：

```java
public class Test02 {
    public static void main(String[] args) {
        Zi z = new Zi();
        z.method();//就近原则,子类有就使用子类的,否则使用父类的//zi
    }
}

class Fu {
    public static void method(){
        System.out.println("传家宝");
//        return;
    }
}

class Zi extends Fu{//想使用父类的,又想有子类特有的,目的,为了让子类比父类更加强大,方法重写,应用场景
    //能够继承拿到然后在子类重写一遍
    public static void method(){
        //想在子类里面使用父类里面的东西,super,超类的,父类的
        //super.method();//表示调用使用父类里面的method方法
        //想使用父类的静态的东西,父类名.
        Fu.method();

        System.out.println("学好Java月薪过万");
    }
}

//class Fu {
//    public void method(){
//        System.out.println("传家宝");
//    }
//}
//
//class Zi extends Fu{//想使用父类的,又想有子类特有的,目的,为了让子类比父类更加强大,方法重写,应用场景
//    //能够继承拿到然后在子类重写一遍
//    public void method(){
//        //想在子类里面使用父类里面的东西,super,超类的,父类的
//        super.method();//表示调用使用父类里面的method方法
//
//
//        System.out.println("学好Java月薪过万");
//    }
//}
```

> 小贴士：这里重写时，用到super.父类成员方法，表示调用父类的成员方法。

### 注意事项//记忆

1. 2.子类重写方法的访问权限要大于或者等于父类(子类要比父类更加强大,强大到访问权限都比父类强大,不能比父类弱)
   					访问权限从小到大排序:private(私有仅仅在本类中被访问)-默认什么都不写(默认可以在同一个包下被访问,巧记默认同胞)-
   					protected(受保护的,只能给子类去访问不管是否同包)-public(公有在哪里都可以访问,公有秒杀)
2. 子类方法覆盖父类方法，返回值类型、函数名和参数列表都要一模一样。

## 1.5 继承后的特点——构造方法//记忆

当类之间产生了关系，其中各类中的构造方法，又产生了哪些影响呢？

首先我们要回忆两个事情，构造方法的定义格式和作用。

1. 构造方法的名字是与类名一致的。所以子类是无法继承父类构造方法的。
2. 构造方法的作用是初始化成员变量的。所以子类的初始化过程中，必须先执行父类的初始化动作。子类的构造方法中默认有一个`super()` ，表示调用父类的构造方法，父类成员变量初始化后，才可以给子类使用。代码如下：

```java
public class Test04 {
    public static void main(String[] args) {
        Erzi z = new Erzi();
        System.out.println(z.i);//0,父类数据,子类创建对象的时候,才给它赋值
    }
}

class Fuqin{
    int i;//0
    public Fuqin(){
//        System.out.println("父类的构造方法");//做其他东西
        i = 666;//给成员变量赋值
    }

    public Fuqin(int j){//j = 888;
        i = j;
    }
}

class Erzi extends Fuqin{
    public Erzi(){
        //子类的构造方法中默认有一个super() ，表示调用父类的构造方法,不写也是写,系统给你写
//        super();//只要你写了,就按照你写的走
          super(888);//super()无参没有,手动调用父类有参构造方法,是int 变量
//        System.out.println(666);
    }
}
//子类的构造方法默认会通过super()访问父类的构造方法目的是让了创建子类对象的时候给父类数据进行初始化比如给成员变量赋值或者做其他东西
```



## 1.6 super和this

### 父类空间优先于子类对象产生

在每次创建子类对象时，先初始化父类空间，再创建其子类对象本身。目的在于子类对象中包含了其对应的父类空间，便可以包含其父类的成员，如果父类成员非private修饰，则子类可以随意使用父类成员。Class C extend P{}

![](img/2.jpg)

### super和this的含义//记忆

* **super** ：代表父类的**存储空间标识**(可以理解为父类的引用)


* **this** ：代表**当前对象的引用**(谁调用就代表谁)。

### super和this的用法//记忆

1. 访问成员

```java
this.成员变量    	--    本类的或者父类的,看就近原则就可以了
super.成员变量    	--    父类的

this.成员方法名()  	--    本类的或者父类的,看就近原则就可以了
super.成员方法名()   --    父类的
```

用法演示，代码如下：

```java
class Animal {
    public void eat() {
        System.out.println("animal : eat");
    }
}
 
class Cat extends Animal {
    public void eat() {
        System.out.println("cat : eat");
    }
    
    public void eatTest() {
        this.eat();   // this  调用本类的方法
        super.eat();  // super 调用父类的方法
    }
}
 
public class ExtendsDemo08 {
    public static void main(String[] args) {
        Animal a = new Animal();
        a.eat();
        
        Cat c = new Cat();
        c.eatTest();
    }
}

输出结果为：
animal : eat
cat : eat
animal : eat
```

2. 访问构造方法//记忆

```java
this(...)    	--    本类的构造方法
super(...)   	--    父类的构造方法
```

> 子类的每个构造方法中均有默认的super()，调用父类的空参构造。手动调用父类构造会覆盖默认的super(...)。
>
> super() 和 this() 都必须是在构造方法的第一行，所以不能同时出现。

## 1.7 继承的特点//记忆

1. Java只支持单继承，不支持多继承。

```java
//一个类只能有一个父类，不可以有多个父类,即继承是亲生关系,一个孩子只能有一个亲爹
class C extends A{} 	//ok
class C extends A，B...	//error,报错
```

2. Java支持多层继承(继承体系)。

```java
//相当于现实生活中的子父爷关系
class A{}
class A extends B{}
class B extends C{}
//A间接继承了C,可以使用C里面可以继承过来的东西,非私有成员变量和成员方法
```



# 第二章 抽象类

## 2.1 概述

### 由来

父类中的方法，被它的子类们重写，子类各自的实现都不尽相同。那么父类的方法声明和方法主体{}，只有声明还有意义，而方法主体{}则没有存在的意义了。我们把没有方法主体{}的方法称为**抽象方法**。Java语法规定，包含抽象方法的类就是**抽象类**。

### 定义

* **抽象方法** ： 没有方法体的方法。
* **抽象类**：包含抽象方法的类,但是更准备的说法应该是用abstract修饰的类就是抽象类,抽象类不一定有抽象方法//记忆

## 2.2 abstract使用格式,抽象的

### 抽象方法

使用`abstract` 关键字修饰方法，该方法就成了抽象方法，抽象方法只包含一个方法名，而没有方法体。

定义格式：

```java
修饰符 abstract 返回值类型 方法名 (参数列表)；
```

代码举例：

```java
public abstract void run()；
```

### 抽象类

如果一个类包含抽象方法，那么该类必须是抽象类。

定义格式：

```java
abstract class 类名字 { 
  
}
```

代码举例：

```java
public abstract class Animal {
    public abstract void run()；
}
```

### 抽象的使用//记忆

继承抽象类的子类**必须重写父类所有的抽象方法**。否则，该子类也必须声明为抽象类。最终，必须有子类实现该父类的抽象方法，否则，从最初的父类到最终的子类都不能创建对象，失去意义。

代码举例：

```java
public class Test06 {
    public static void main(String[] args) {
       // Animal a = new Animal();//抽象类不能创建对象,抽象类,就是抽象的,不是具体的,没有具体的对象,不能创建对象

//        Cat c = new Cat();//Cat抽象类不能创建对象
//        c.eat();
//
//        Sheep d = new Sheep();
//        d.eat();

        Cat c = new Cat();
        c.eat();//就近原则

        System.out.println(c.i);
        c.show();

    }
}

//包含抽象方法的类,但是更准备的说法应该是用abstract修饰的类就是抽象类,抽象类不一定有抽象方法
abstract class Animal {//有抽象方法的类,是抽象类,加上标记abstract关键字
    //所有动物都吃鱼?不合理,所有都会吃饭的功能,但是具体怎么吃,我不知道,不太清楚,对于我来说就是抽象的,抽象方法
    public abstract void eat();//{}抽象方法{}去掉加上标记abstract关键字,未实现的方法
//    public abstract void eat2();//{}抽象方法{}去掉加上标记abstract关键字,未实现的方法

    int i = 666;

    public  void show(){
        System.out.println("show");
    }
}

class Cat extends Animal {//想成为抽象类的子类,要么也是抽象类(没有意义),要么重写抽象类里面所有的抽象方法,alt enter

    @Override
    public void eat() {//重写抽象方法eat,增加{}方法体,里面做事情
        System.out.println("吃鱼");
    }
}
//
//class Sheep extends Animal {
//
//}
```

此时的方法重写，是子类对父类抽象方法的完成实现，我们将这种方法重写的操作，也叫做**实现方法**。

## 2.3 注意事项//记忆

关于抽象类的使用，以下为语法上要注意的细节，虽然条目较多，但若理解了抽象的本质，无需死记硬背。

1. 抽象类**不能创建对象**，如果创建，编译无法通过而报错。只能创建其非抽象子类的对象。

   > 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体{}，做不了事情,没有意义。

2. 抽象类中，可以有构造方法，是供子类创建对象时，初始化父类成员使用的。

   > 理解：子类的构造方法中，有默认的super()，需要访问父类构造方法。

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

   > 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设计。

4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，否则，编译无法通过而报错。除非该子类也是抽象类。 

   > 理解：假设不重写所有抽象方法，则类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有意义。

# 第三章 继承的综合案例

## 3.1 综合案例：群主发普通红包

群主发普通红包。某群有多名成员，群主给成员发普通红包。普通红包的规则：

1. 群主的一笔金额，从群主余额中扣除，平均分成n等份，让成员领取。
2. 成员领取红包后，保存到成员余额中。

请根据描述，完成案例中所有类的定义以及指定类之间的继承关系，并完成发红包的操作。

## 3.2 案例分析

根据描述分析，得出如下继承体系：

![](img/3.jpg) 

## 3.3 案例实现

~~~java
import java.util.ArrayList;
import java.util.Random;
public class Test {
    public static void main(String[] args) {
        Sender s = new Sender("群主", 100);
        ArrayList<Integer> al = s.send(20, 3);

        if (al==null){
            System.out.println("余额不足不能发红包");
            return;
        }

        Getter g = new Getter("one", 0);
        Getter g2 = new Getter("two", 0);
        Getter g3 = new Getter("three", 0);

        g.get(al);
        g2.get(al);
        g3.get(al);

        s.show();
        g.show();
        g2.show();
        g3.show();
    }
}

class Getter extends Client{//群成员众屌丝也是微信的客户
    //alt insert
    public Getter() {
    }

    public Getter(String name, int money) {
        super(name, money);
    }

    //抢红包,得到分配好的集合,随机一个集合索引拿出一个红包即移除上面集合中的一个红包返回,给余额设置值
    public void get(ArrayList<Integer> al){
        Random r = new Random();
        int index = r.nextInt(al.size());//0-长度减1,索引

        int money = al.remove(index);
        setMoney(money);
    }
}

class Sender extends Client {//群主也是微信的客户
    //alt insert
    public Sender() {
    }

    public Sender(String name, int money) {
        super(name, money);
    }

    //发红包,发多少钱,分多少个红包,把分配好的红包存到集合里面返回,给别人抢
    public ArrayList<Integer> send(int money, int count){
        //判断钱够不够,不够返回一个标记,够就扣钱,给余额重新赋值
        if (money>getMoney()){
            return null;
        }

        setMoney(getMoney()-money);

        ArrayList<Integer> al = new ArrayList();
        int avg = money/count;//每个红包多少钱
        int mod = money%count;//平均多出的小钱

        for (int i = 0; i < count-1; i++) {
            al.add(avg);
        }

        if (mod==0){
            al.add(avg);
        }else {
            al.add(avg + mod);
        }

        return al;
    }
}

class Client {//客户
    private String name;
    private int money;

    //alt insert
    public Client() {
    } 

    public Client(String name, int money) {
        this.name = name;
        this.money = money;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }

    //查看姓名和钱
    public void show(){
        System.out.println(name+"有多少钱:"+money);
    }
}
~~~

> 课后请同学自己思考并完成扩展需求。
>
> 案例扩展：
>
> 1. 如果成员的余额不为0呢，将如何处理？
> 2. 如果群主想输入带小数的金额呢，将如何处理？

