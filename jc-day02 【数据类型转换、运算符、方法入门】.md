# day02 【数据类型转换、运算符、方法入门】

## 今日内容

- 数据类型转换
- 算数运算符
- 比较运算符
- 逻辑运算符
- 三元运算符
- 简单方法定义(就是写一个方法)和调用(就是把写好的方法使用起来)

## 教学目标

-    [ ] 理解数据类型的强制转换
-    [ ] 理解数据类型的自动转换
-    [ ] 了解ASCII编码表
-    [ ] 理解int类型和char类型的运算原理
-    [ ] 理解运算符++ --的运算方式
-    [ ] 理解+符号在字符串中的作用
-    [ ] 理解比较运算符
-    [ ] 理解逻辑运算符
-    [ ] 掌握三元运算符的格式和计算结果
-    [ ] 了解方法的概念
-    [ ] 掌握无返回值无参数方法的定义格式
-    [ ] 了解方法定义的注意事项
# 第一章 数据类型转换

Java程序中要求参与的计算的数据，必须要保证数据类型的一致性，如果数据类型不一致将发生类型的转换。

## 1.1 自动转换(也叫隐式类型转换,系统悄悄自动做的你看不到)

~~~java
public class Test {
	public static void main(String[] abc){
		int i = (int)23.4;//手动做,强制类型转换,把大压缩成小的
		//注释,不会执行,无效代码,给人看的,解释说明我写其他代码
		//系统输出打印

		double d = 666;//666int-double666.0,系统,悄悄给你做,保持数据类型的一致性,隐式类型转换,类型提升,把小的数据类变成大的数据类型
		System.out.println(d);//666.0小括号只能打印的是变量名或者变量的值(常量),通过变量名也是为了得到变量的值,本质是个值
	}
}
~~~



 一个`int` 类型变量和一个`byte`类型变量进行加法运算， 结果会是什么数据类型？ 

```java
int i = 1; 
byte b = 2; 
```

运算结果，变量的类型将是`int` 类型，这就是出现了数据类型的自动类型转换现象。

* **自动转换**：将`取值范围小的类型`自动提升为`取值范围大的类型`(所以还叫类型提升) 。

```java
public static void main(String[] args) {
    int i = 1;
    byte b = 2;
    
  	// byte x = b + i; // 报错
    
    //int类型和byte类型运算，结果是int类型
    int j = b + i;//byte2-int2,自动完成,隐式类型转换,类型提升,由小的类型byte提升为大的类型int
    System.out.println(j);//3,规则,必须遵循,记忆,应用
}
```

### 转换原理图解

`byte` 类型内存占有1个字节，在和`int` 类型运算时会提升为`int`类型 ，自动补充3个字节，因此计算后的结果还是`int` 类型。

![](img/类型自动提升.jpg)

同样道理，当一个`int` 类型变量和一个`double` 变量运算时，`int` 类型将会自动提升为`double` 类型进行运算。

```java
public static void main(String[] args) {
    int i = 1;
    double d = 2.5;
    
    //int类型和double类型运算，结果是double类型
    //int类型会提升为double类型
    double e = d+i;//iint1-double1.0
    System.out.println(e);//3.5
}
```
### 转换规则,需要记忆!!!

范围小的类型向范围大的类型提升,才能给大的运算,保持数据类型一致性，注意,`byte、short、char` 运算时直接提升为`int` 。

```java
byte、short、char-->int-->long-->float-->double//数据类型从小到大的排序,需要记忆,巧记,整数和小数中间插入char
```



## 1.2 强制转换	

将`1.5` 赋值到`int` 类型变量会发生什么？产生编译失败，肯定无法赋值。

```java
int i = 1.5; // 错误
```

`double` 类型内存8个字节，`int` 类型内存4个字节。`1.5` 是`double` 类型，取值范围大于`int` 。可以理解为`double` 是8升的水壶，`int` 是4升的水壶，不能把大水壶中的水直接放进小水壶去。

想要赋值成功，只有通过强制类型转换，将`double` 类型强制转换成`int` 类型才能赋值。

* **强制类型转换**：将`取值范围大的类型`强制转换成`取值范围小的类型`。

 比较而言，自动转换是Java自动执行的，而强制转换需要我们自己手动执行。

**转换格式：**

```java
数据类型 变量名 = （数据类型）被转数据值；
```

将`1.5` 赋值到`int` 类型，代码修改为：

```java
// double类型数据强制转成int类型，直接去掉小数点。
int i = (int)1.5;//1.5double-int1
System.out.println(i);//1
```

同样道理，当一个`short`类型与`1`相加，我们知道会类型提升，但是还想给结果赋值给short类型变量，就需要强制转换。

```java
public static void main(String[] args) {
     //short类型变量，内存中2个字节
     short s = 1;
     /*
       出现编译失败
       s和1做运算的时候，1是int类型，s会被提升为int类型
       s+1后的结果是int类型，将结果在赋值会short类型时发生错误
       short内存2个字节，int类型4个字节
       必须将int强制转成short才能完成赋值
     */
     s = s + 1;//编译失败
         
     s = (short)(s+1);//编译成功
     System.out.println(s);//2
}
```

### 转换原理图解

![](img/类型强制转换.jpg)



### 强转要注意的

- 浮点 小数转成整数，直接取消小数点,    可能造成数据损失精度。
- `int` 强制转成`short` 砍掉了2个字节，可能造成**数据溢出**。

```java
//小数即浮点转成整数，直接取消小数点，可能造成数据损失精度。
int i = (int) 23.4;//double23.4-int23
System.out.println(i);//23,损失精度

int i2 = (int) 5.0;
System.out.println(i2);//5,没有损失精度,所以上面说可能↑

//定义s为short范围内最大值
short s = 32767;//最大值
//运算后，强制转换，砍掉2个字节后会出现想要的结果
s = (short)(s + 10);//+1变成最小值-32768,再加9就是-32759
System.out.println(s);//-32759
//数据溢出:最大值加1不能再大就变成最小值,最小值-1不能再减就变成最大值,保持运算得到结果
```



## 1.3 ASCII编码表,计算机底层都是0和1,无法直接表示字符,所以每一个字符进行编码,比如a字符对应一个编码是97,97转换成二进制的0和1就可以存起来,说白了就是一种编号思想

```java
public static void main(String[] args) {
  //字符类型变量
  char c = 'a';
  int i = 1;
    
  //字符类型和int类型计算
  System.out.println(c+i);//输出结果是98,c是char类型,参与运算时会自动提示为int类型,即char'a'-int97
    
  char c2 = 'a';
  char c3 = 'a';
   
  //字符类型和int类型计算
  System.out.println(c2+c3);//char-int97 ,char-int97 //int194
}
```

在计算机的内部都是二进制的0、1数据，如何让计算机可以直接识别人类文字的问题呢？就产生出了编码表的概念。

* **编码表** ：就是将人类的文字和一个十进制数进行对应起来组成一张表格。

  人们就规定：

  | 字符  |  数值  |
  | :---: | :----: |
  | **0** | **48** |
  |   9   |   57   |
  | **A** | **65** |
  |   Z   |   90   |
  | **a** | **97** |
  |   z   |  122   |

  - 将所有的英文字母，数字，符号都和十进制进行了对应，因此产生了世界上第一张编码表ASCII（                     			        

  American Standard Code for Information Interchange 美国标准信息交换码）。

> 小贴士：
>
> 在char类型和int类型计算的过程中，char类型的字符先查询编码表，得到97，再和1求和，结果为98。char类型提升为了int类型。char类型内存2个字节，int类型内存4个字节。

一个同时把自动类型即隐式类型和强制类型转换结合在一起的例子:a变成A

~~~java
char a = 'a';//97
char c = (char)(a-32);//65,char(int97)-int=64;
System.out.println(c);//A

char a = '你';//97
System.out.println(a+0);//97,char(int97)+int0=97,20320,unicode,万国码表
~~~



# 第二章 运算符

## 2.1 算数运算符

| 算数运算符包括： |                                                              |
| ---------------- | ------------------------------------------------------------ |
| `+`              | 加法运算，或者表示字符串里面的连接运算                       |
| `-`              | 减法运算                                                     |
| `*`              | 乘法运算                                                     |
| `/`              | 除法运算,整数除以整数,结果还是整数,java的规则,保持数据类型的一致性 |
| `%`              | 取模运算，即两个数字相除取余数,求余数,注意事项,取模求余数,它的结果只跟左边的符号相关,跟右边符号无关 |
| `++` 、  `--`    | 自增自减运算                                                 |


注意,Java中，整数使用以上运算符，无论怎么计算，也不会得到小数。

```java
public static void main(String[] args) {
  	int i = 1234;
  	System.out.println(i/1000*1000);//整数除以整数,结果还是整数,所以i/1000结果是1,最终计算结果是1000
    
    int a = 10;
    int b = 3;
    int c = a/b;//int/int=int=3;
    System.out.println(c);//3

    System.out.println(10/3);//3
    
    int a2 = 10;
    int b2 = 3;
    int c2 = a2%b2;//a/b的余数1
    System.out.println(c2);//1//注意事项,取模求余数,它的结果只跟左边的符号相关,跟右边符号无关
    
    int a22 = -10;
    int b22 = -3;
    int c22 = a22%b22;//a/b的余数1

    //注意事项,取模求余数,它的结果只跟左边的符号相关,跟右边符号无关
    System.out.println(c22);//-1
    
    //跟别人参与运算
    //int c = ++a + 1;//++在前肯定优先,先自增得到结果,在跟别人参与运算
    //System.out.println(c);//668

    int c = a++ + 1;//667,++在后肯定不优先,先放一放,,先跟别人参与运算完毕得到结果,自己再自增,这里自增都是表示加1的意思
    System.out.println(c);//667
    
    int a = 666;
    //++a;//a=a+1;//667,单独使用,就是加1的意思,自增
    //a++;//a=a+1;//667,单独使用,就是加1的意思,自增

    //跟别人参与运算
    //int c = ++a;//++在前肯定优先,先自增得到结果,在跟别人参与运算
    //System.out.println(c);//667,=赋值号也是一种运算,这里的别人是c,不是单独使用!!!

    int c = a++;//,++在后肯定不优先,先放一放,,先跟别人参与运算完毕得到结果,自己再自增,这里自增都是表示加1的意思
    System.out.println(c);//666,=赋值号也是一种运算,这里的别人是c,不是单独使用!!!
}
```

- `++`  **运算，变量自己增长1**。反之，`--` 运算，变量自己减少1，用法与`++` 一致。

  - 独立运算：

    - 变量在独立运算时，`前++`和`后++`没有区别 。
    - 变量`前++`   ：例如 `++i` 。
    - 变量`后++`   ：例如 `i++` 。

  - 混合运算：

    * 和其他变量放在一起，`前++`和`后++`就产生了不同。

    - 变量`前++` ：变量a自己加1，将加1后的结果,再跟别人参与运算，所以下面的a和b的结果都是2。

    ```java
    public static void main(String[] args) {
        int a = 1;
        int b = ++a;//a先++增加1,得到结果2,然后跟别人参与赋值运算,所以b是2
        System.out.println(a);//计算结果是2
        System.out.println(b);//计算结果是2
    }
    ```

    - 变量`后++` ：变量a先把自己的值1，赋值给变量b，此时变量b的值就是1，变量a自己再加1。a的结果是2，b的结果是1。

    ```java
    public static void main(String[] args) {
        int a = 1;
        int b = a++;//++在后,先跟别人参数运算,得到完毕的结果,所以b是1,然后自己在++增加1,a是2
        System.out.println(a);//计算结果是2
        System.out.println(b);//计算结果是1
        
        
    }
    ```



- `+` 符号在字符串中的操作：表示字符串连接符,不是传统意义上的+号
  - `+` 符号在遇到字符串的时候，表示**连接、拼接**的含义,即串起来的意思。
  - "a"+"b"可以读作a串上b,所以得到的结果是“ab”，+连接含义,理解为相当于羊肉串的棍子,把东西串起来
  - 只要有其中一个是字符串,不管位置前后,通过+号相连接,得到的结果还是字符串!!!

```java
public static void main(String[] args){
   //只要有其中一个是字符串,不管位置前后,通过+号相连接,得到的结果还是字符串!!!
    //运算的顺序一般是从左到右,想先运算用()小括号围起来,提高运算优先级
    //如果是真的=赋值号,优先级几乎最低,先算右边再给左边的变量赋值
    System.out.println(5+5+"5+5=");//105+5=
    System.out.println("5+5="+5+5);//5+5=55
    System.out.println("5+5="+(5+5));//5+5=10
}
```



## 2.2 赋值运算符,优先级几乎是最低的,先算=右边数据,给左边的变量赋值,要求左边是个变量,不能是常量(5),比如5=5;错误的,正确的是int a = 5;

| 赋值运算符包括： |                                                        |
| ---------------- | ------------------------------------------------------ |
| `=`              | 赋值号,可以理解为等于号,下面都是一样的理解             |
| `+=`             | 加等于,把符号左右两边的数据相加的结果,赋值给左边的变量 |
| `-=`             | 减等于                                                 |
| `*=`             | 乘等于                                                 |
| `/=`             | 除等于                                                 |
| `%=`             | 取模等,求余数                                          |

* 赋值运算符，就是将符号右边的值，赋值给左边的变量。
* 换句话说,=赋值号先算出右边的结果,然后给左边的的变量进行赋值


```java
public static void main(String[] args){
   //赋值运算符,优先级几乎是最低的,先算=右边数据,给左边的变量赋值,要求左边是个变量,不能是常量(5),
		//比如5=5;错误的,正确的是int a = 5;
		//5 = 5;//编译报错,语法问题,不符合java的规则

		//int a = 5;
		//System.out.println(a);//5

		int a = 5;
		a+=5;//a = a+5;//=赋值号先算右边整体,再跟左边的变量赋值,说白,把左右两边的数据相加的结果,赋值给左边的变量
		System.out.println(a);//10
}
```



## 2.3 比较运算符(又叫关系运算符),比较,关系,大于或者小于...

| 比较运算符包括： |                                                              |
| ---------------- | ------------------------------------------------------------ |
| `==`             | 等于,比较符号两边数据是否相等，相等结果是true。              |
| `<`              | 小于,比较符号左边的数据是否小于右边的数据，如果小于结果是true。 |
| `>`              | 大于,比较符号左边的数据是否大于右边的数据，如果大于结果是true。 |
| `<=`             | 小于或者等于,比较符号左边的数据是否小于或者等于右边的数据，如果大于结果是false。 |
| `>=`             | 大于或者等于,比较符号左边的数据是否大于或者等于右边的数据，如果小于结果是false。 |
| `！=`            | 不等于，如果符号两边的数据不相等，结果是true。               |

* 比较运算符，是两个数据之间进行比较的运算，运算结果都是布尔值`true`或者`false` 。

```java
public static void main(String[] args) {
   System.out.println(1==1);//true,等于号,1等于1是真的吗?结果就是真,true,如果是假的,结果就是假,false,最终是布尔类型
    System.out.println(1<2);//true,小于号
    System.out.println(3>4);//false,大于号
    System.out.println(3<=4);//true,小于或者等于号
    System.out.println(3>=4);//false,大于或者等于号
    System.out.println(3!=4);//true,不等于号
}
```



## 2.4 逻辑运算符,并且,或者,取反非,运算完毕的结果也是布尔类型

| 逻辑运算符包括：                    |                                                              |
| ----------------------------------- | ------------------------------------------------------------ |
| `&&`  短路与,与,并且的意思          | 1. 两边都是true，结果是true  <br />2. 一边是false，结果是false  <br />短路特点：符号左边是false，右边不再运算 |
| `||`  短路或,或,或者的意思          | 1. 两边都是false，结果是false  <br />2. 一边是true，结果是true  <br />短路特点： 符号左边是true，右边不再运算 |
| `！`   非,取反,原来是真的取反就是假 | 1. ! true 结果是false<br />2. ! false结果是true              |

* 逻辑运算符，有要求的,不管写法简单还是复杂,结果一定是布尔类型的数据，运算结果都是布尔值`true`或者`false`

```java
public static void main(String[] args)  {
    //不会,记忆下面的口诀即可,但是重要的还是理解记忆,你理解并且是什么意思,或者是什么意思,就明白了:
    //&&,并且的意思,要求两边同时成立,整个结果连接起来才成立是真,巧记为,同为真时且为真,其他情况都为假
    System.out.println(true && true);//true
    System.out.println(true && false);//false
    System.out.println(false && true);//false，右边不计算,运算需要时间,调高效率,短路
    System.out.println(false && false);//false,右边不计算,运算需要时间,调高效率,短路
  
   //||,或者的意思,只有有一个成立,整个结果连接起来就是成立为真,巧记为,同为假时或为假,其他情况都为真
    System.out.println(true || true);//true,右边不计算,运算需要时间,调高效率,短路
    System.out.println(true || false);//true,右边不计算,运算需要时间,调高效率,短路
    System.out.println(false || true);//
    System.out.println(false || false);//
    //||,或者的意思,只有有一个成立,整个结果连接起来就是成立为真,巧记为,同为假时或为假,其他情况都为真
  
    System.out.println(!false);//true
    System.out.println(!true);//false
    System.out.println(!!true);//true,对一个数取反偶数次,结果还是本身
    System.out.println(!!!true);//false,对一个数取反偶数次,结果还是本身
    
    //&,|,规律口诀 是一样,只是没有短路效果,不管啥情况都要参与运算,效率低,一般不用了
}
```



## 2.5 三元运算符,也是运算符,运算符完毕就应该得到一个结果,所以我可以定义一个变量来接收或者说存储结果的值

* 三元运算符格式：

```java
 数据类型 变量名 = 布尔类型表达式？结果1：结果2
```

- 三元运算符计算方式：
  - 布尔类型表达式结果是true，三元运算符整体结果为结果1，赋值给变量。
  - 布尔类型表达式结果是false，三元运算符整体结果为结果2，赋值给变量。

```java
public static void main(String[] args) {
    int i = (1==2 ? 100 : 200);
    System.out.println(i);//200
    int j = (3<=4 ? 500 : 600);
    System.out.println(j);//500
    
    //三元运算符,也是运算符,运算符完毕就应该得到一个结果,所以我可以定义一个变量来接收或者说存储结果的值
    int a = 666;
    int b = 888;
    int c = (a>b)? a:b;//a>b,如果是真结果是true,整个三元(目)运算符结果就是a,否则是b;
    System.out.println(c);//888
}
```



# 第三章 方法入门

## 3.1 概述

我们在学习运算符的时候，都为每个运算符单独的创建一个新的类和main方法，我们会发现这样编写代码非常的繁琐，而且重复的代码过多。能否避免这些重复的代码呢，就需要使用方法来实现。

一类事物,写一个类来模拟,一类事物一个功能,写一个方法来模拟,方法应该写在类中{}里面

- **方法：**就是将一个**功能**抽取出来，把代码单独定义在一个大括号内{}，形成一个单独的功能。


当我们需要这个功能的时候，就可以去调用(使用)。这样即实现了代码的复用性，也解决了代码冗余的现象。

## 3.2 方法的定义,就是写一个方法,没有使用,只是摆在那里而已

* 定义格式： 

```java
修饰符 返回值类型 方法名 （参数列表）｛
    	代码...	
   		return ;
｝
```

- 定义格式解释：
  - 修饰符： 目前固定写法 `public static` 。
  - 返回值类型： 目前固定写法 `void` ，其他返回值类型在后面的课程讲解。
  - 方法名：为我们定义的方法起名，满足标识符的规范，用来调用方法。
  - 参数列表： 目前无参数， 带有参数的方法在后面的课程讲解。
  - return：方法结束。因为返回值类型是void，方法大括号内的return可以不写(后面解释返回值是什么)。
- 举例： 

```java
public static void methodName() {
    //一类事物,写一个类来模拟,一类事物一个功能,写一个方法来模拟,方法应该写在类中{}里面
	//方法：就是将一个功能抽取出来，把代码单独定义在一个大括号内{}，形成一个单独的功能。

  	System.out.println("这是一个方法");
    //return;这句话不写也是写,系统给你写,return,返回来的意思,或者说,带回,回来的意思,从哪里调用就回到哪
}
```

## 3.3 方法的调用,就是调用一个方法,或者说使用一个方法,就跑到方法的{}里面去做事情

方法在定义完毕后，方法不会自己运行，必须被调用(使用)才能执行，我们可以在主方法main中,来调用我们自己定义好的方法。在主方法中，直接写要调用的方法名字加()就可以了,分号;表示语句的结束而已!!!

```java
public static void main(String[] args) {//main主方法是程序的入口,也是出口,从这开始执行,也从这里结束
    //调用定义的方法method
    method();
}

//定义方法，被main方法调用
public static void method() {
  	System.out.println("自己定义的方法，需要被main调用运行");
}

//课堂笔记,看这个:
public class Test {
	public static void main(String[] abc){//jvm调用,使用,运行程序,main主方法是程序的入口,也是出口,从这开始执行,也从这里结束
		//一类事物,写一个类来模拟,一类事物一个功能,写一个方法来模拟,方法应该写在类中{}里面
		//方法：就是将一个功能抽取出来，把代码单独定义在一个大括号内{}，形成一个单独的功能。

		//方法的调用,就是调用一个方法,或者说使用一个方法,就跑到方法的{}里面去做事情,格式,方法名();
		method();
		method();
		method();//方法的作用:少写了很多代码,实现一样的功能,提高代码复用性(代码重复使用性能)
		
		System.out.println("666");
		//return;结束方法的,这句话不写也是写,系统给你写,return,返回来的意思,或者说,带回,回来的意思,从哪里调用就回到哪
	}

	//方法的定义,就是写一个方法,没有使用,只是摆在那里而已
	public static void method(){//jvm调用,使用,运行程序,main主方法是程序的入口,也是出口,从这开始执行,也从这里结束
		System.out.println("我爱你");
		System.out.println("我爱你");
		System.out.println("我爱你");
		//return;结束方法的,这句话不写也是写,系统给你写,return,返回来的意思,或者说,带回,回来的意思,从哪里调用就回到哪
	}
}
```



## 3.4 调用练习

将三元运算符代码抽取到自定义的方法中，并调用。

```java
public static void main(String[] args) {
    //调用定义的方法operator
    operator();
}

//定义方法，方法中定义三元运算符
public static void operator() {
    int i = 0;
    i = (1==2 ? 100:200);
    System.out.println(i);
    
    int j = 0 ;
    j = (3<=4 ? 500:600);
    System.out.println(j);
}
```


## 3.5 注意事项

- 方法定义(就是写一个方法)注意事项：

  - 方法必须定义类中{},方法的外面

  - 方法里面不能再写一个方法

  - **理解**,在java里面一类事物,写一个类来模拟,而方法是一类事物里面的一个功能,所以要写在类中{}里面,

    既然是一个功能,其他方法代表其他功能,功能与功能应该独立开来,所以不能在一个方法里面再写一个方法

```java
public class Demo {
    public static void main(String[] args){
        
    }
    
    //正确写法，写在类中{},方法的外面
    public static void method(){}
}
```

```java
public class Demo {
 	
    public static void main(String[] args){
        //错误写法，不能在方法里面再写一个方法
        public static void method(){}
    }
    
    
}
```



# 第四章 JShell脚本工具

### JShell脚本工具,是JDK9的新特性

什么时候会用到`JShell`这个工具呢?当我们编写的代码非常少的时候，而又不想编写类，main方法时，也不想去编译和运行时，这时,可以使用JShell工具快速来代替。

启动JShell工具，在DOS命令行直接输入**JShell**命令(注意,jshell命令大小写都可以)。

![](img/jshell开启.jpg)

接下来可以编写Java代码，无需写类和方法，直接写方法中的代码即可，同时无需编译和运行，直接回车即可

![](img/jshell使用.jpg)

> 小贴士:
>
> JShell工具，只适合片段代码的测试，开发更多内容，建议编写在方法中。



# 第五章 扩展知识点

## 5.1 +=符号扩展,隐藏了自动的强制类型转换,不写也是写,系统写!

下面的程序有问题吗？

```java
public static void main(String[] args){
  short s = 1;
  s+=1;
  System.out.println(s);
}

////+=符号扩展,隐藏了自动的强制类型转换,不写也是写,系统写!
		  short s = 1;
		  //s=s+1;//报错,int+int=int;
		  //s=(short)(s+1);//以前强制手段

		  s+=1;//s=s+1;看起是这个,实际上是这个 s=(short)(s+1);,隐藏自动的强制类型转换,不写也是写,系统帮我写
		  System.out.println(s);//2
```

分析： `s += 1` 逻辑上看作是`s = s + 1` 计算结果被提升为int类型，再向short类型赋值时发生错误，因为不能将取值范围大的类型赋值到取值范围小的类型。但是，`s=s+1进行两次运算`，**`+=` 是一个运算符，只运算一次，并带有强制转换的特点**，**也就是说`s += 1` 就是`s = (short)(s + 1)`**，因此程序没有问题,编译通过，运行结果是2.



## 5.2 常量和变量的运算

下面的程序有问题吗？

```java
public static void main(String[] args){
 	byte b1=1;
    byte b2=2;
    //byte b3=1 + 2;//编译阶段,1,2都是常量,编译器有个常量优化机制,实际是3
    
    //下面编译报错,编译阶段还没运行,是变量无法确定它的值
    byte b4=b1 + b2;//变量,编译器无法确定他具体的值,认为就是变量有可能发生变化,byte+byte=int+int=int;
  
    //System.out.println(b3);//3
    System.out.println(b4);//	
}
```
分析：`b3 = 1 + 2` ，`1 `和 `2 ` 是常量，为固定不变的数据，在编译的时候（编译器javac），已经确定了`1+2` 的结果并没有超过byte类型的取值范围，可以赋值给变量`b3` ，因此`b3=1 + 2`是正确的。

反之，`b4 = b2 + b3`，`b2` 和 `b3` 是变量，变量的值是可能变化的，在编译的时候，编译器javac不确定b2+b3的结果是什么，因此会将结果以int类型进行处理，所以int类型不能赋值给byte类型，因此编译失败。

在jshell中体现：

![](img/扩展.jpg)