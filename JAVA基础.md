## 1. 环境安装

### 1.1 jdk下载
[https://www.jdkdownload.com)](https://www.jdkdownload.com/)

### 1.2 配置环境变量
* 系统环境变量处新建环境变量名字为 **JAVA_HOME**
* JAVA_HOME路径为java安装路径
* 配置path变量`%JAVA_HOME%\bin`
* 配置path变量`%JAVA_HOME%\jre\bin`

### 1.3 安装检测
dos命令窗口输入
```java
java -version
```
不报错则表示安装成功

---  
>向世界问好
1. 新建一个.java后缀的java文件
2. 编写代码(类名要与文件名一致)
```java
public class hello{
    public static void main(String[] args){
        System.out.print("hello world");
    }
}
```

3. 编译文件  
cd到文件目录输入: `javac 文件名.java`  
运行完后出现一个class文件  
4. 运行class文件  
dos命令行输入: `java 文件名`
---

## 2. 基础

### 2.1 注释

* `//`　　　&ensp;单行注释
* `/* */`　　多行注释
* `/** */`　&ensp;文档注释

例：
```java
public class Hello {
    public static void main(String[] args){
        //单行注释
        /*多行注释*/
        /**
         * @Description:Hello world
         * @Author:lvcheng
         */
        System.out.println("Hello world");
    }
}
```
### 2.2 变量名
* 首字母是英文字母、$和下划线(不能由数字开头)
* 变量可以由字母、数字和下划线组成
* 不能用Java关键字作为变量名
* 可以用中文作为变量名

![关键字](https://images2015.cnblogs.com/blog/789204/201612/789204-20161228205155054-724919908.png)

### 2.3 数据类型

类型名 | 关键字| 占用内存 | 取值范围
---|---|---|---
字节型 | byte |1字节 |-128~127
短整型 | short |2字节 |-32768~32767
整型 | int |4字节 |-2147483648~2147483647
长整型 | long |8字节 |-9223372036854775808L~9223372036854775807L
单精度浮点型 |float |4字节 |+/-3.4E+38F（6~7 个有效位）
双精度浮点型 |double |8字节 |+/-1.8E+308 (15 个有效位）
字符型 |char |2字节 |ISO 单一字符集
布尔型 |boolean |1字节 |true 或 false

例:
```java
public class demo1 {
    public static void main(String[] args){
        //整型
        int num=10;
        byte num2=20;
        short num3=30;
        long num4=40;
        //浮点型
        float num5=50.1F; //float类型要在数字后面加上F
        double num6=3.1415926;
        //字符型
        char ch1= 'A';
        String ch2="ABC"; //String不是关键词是类
        //布尔型
        boolean b1=true;
        boolean b2=true;
    }
}
```  
  
>据类型拓展
```java
public class demo2 {
    public static void main(String[] args) {
        //二进制0b开头
        int tow = 0b100;
        //八进制0开头
        int eight = 012;
        //十六进制0x开头
        int sixteen = 0x12;
        System.out.println(tow);    //输出结果：4
        System.out.println(eight);  //输出结果：10
        System.out.println(sixteen);//输出结果：18

        char ch1='A';
        char ch2='中';
        System.out.println((int)ch1); //输出结果:65
        System.out.println((int)ch2); //输出结果:20013
    }
}
```
### 2.4 类型转换
转换时尽量将小的转换为大的**避免内存溢出**

```
graph LR
byte,short,char-->int
int-->long
long-->float
float-->double
```

例：
```java
public class demo3 {
    public static void main(String[] args){
        //从低到高自动转换
        int i=128;
        double b=i;
        //从高到低强制转换
        byte n=(byte)i;      //输出-128内存溢出
        //JDK7新特性,数字之间可以加_分割
        int num=1_000_000    //输出1000000
        System.out.println(i); 
    }
}
```
注：
* 不能对布尔类型转换
* 不能转换到别的类型
* 转换的时候主义内存溢出
* 数字之间可以加_分割 

### 2.5 作用域
* 局部变量 ——必须声明和初始化值
* 实例变量 ——从属于对象需要实列化对象后使用
* 类变量　 ——从属于类，加上static关键字
* 常量  　　——定义后不能改变值，加上final关键字

例：
```java
public class demo4 {
    //类变量 static关键字
    static double salary=2500;
    
    //实列变量
    String name;
    int age;
    
    //常量 加上final关键字 这是修饰符不区分前后
    static final double PI=3.14;
    final static double pi=3.14;
    
    public static void main(String[] args) {
        //局部变量
        int i=10;
    }
}

```
### 2.6 运算符
* 算数运算符：+　 -　 *　 /　 %　 ++　 --
* 赋值运算符：＝
* 关系运算符：＞　＜　>=　<=　!=　instanceof
* 逻辑运算符：&&　||　！
* 位运算符：　&　|　^　~　>>　<<　>>>
* 条件运算符：?　:
* 扩展赋值运算符：+=　-=　*=　/=

>IDEA快捷键ctrl+D 复制当前行到下一行
```java
package operator;

public class Demo1 {
    public static void main(String[] args){
        //IDEA快捷键ctrl+D 复制当前行到下一行
        
        //幂运算
        double pow=Math.pow(2,3);
        System.out.print(pow);
        
        //位运算
        /*
        A=0011 1100
        B=0000 1101
        ------------------
        A&B=0000 1100
        A|B=0011 1101
        A^B=0011 0001  //异或操作 相同的是0不相同的是1
        ~B=1111 0010
        
        //运算效率高
        << 左移运算符   *2
        >> 右移运算符   /2
        0000 0001   1
        0000 0010   2
        0000 0100   4
        0000 1000   8
         */
         
        //字符串连接
        int a=10;
        int b=20;
        System.out.println(""+a+b);  //输出1020字符串
        System.out.println(a+b+"");  //输出30数字
    }
}

```
**三元运算符：**
`x ? y : z`  
*如果x为true，则结果为y,如果x为false，结果为z*  

```java
package operator;

public class Demo2 {
    public static void main(String[] args) {
        int a=70;
        String type= a>60?"及格":"不及格";
        System.out.println(type); //输出结果 及格
    }
}
```

### 2.7 包机制

 * 包的本质是一个文件夹  (放在最上面)  
 语法格式：`package package1`
 * 一般将域名倒置作为包名  
 例如：*top.cxy96.blog*
 * 导包  
 语法格式：`import package1`  

[阿里巴巴开发手册](https://www.w3cschool.cn/alibaba_java/)
### 2.8 javadoc

* javadoc命令是用来生成API文档

参数信息:
* @author 作者名
* @version 版本号
* @since 指明需要最早使用的jdk版本
* @param 参数名
* @return 返回值情况
* @throws 异常抛出情况

[API帮助文档](https://www.oracle.com/cn/java/technologies/java-se-api-doc.html)
```java
package top.base;

/**
 * @author  lvchneg
 * @version 1.0
 * @since 1.8
 */
public class demo5 {
    String name;

    /**
     *
     * @param name
     * @return
     * @throws Exception
     */
    public String test(String name)throws Exception{
        return name;
    }
}
```
命令行生成Javadoc文档  
`javadoc -encoding UTF-8 -charset UTF-8 文件名.java`  
IDEA生成javadoc文档  
[https://blog.csdn.net/qq_44122193/article/details/114789427](https://blog.csdn.net/qq_44122193/article/details/114789427)

## 3. 流程控制

### 3.1 用户交互
**JAVA提供了一个工具类可以获取用户的输入。 java.util.Scanner是java5的新特征可以通过Scanner获取用户的输入。**

基本语法:  
`Scanner s=new Scanner(System.in)`

**通过 Scanner类的 next() 和 nextLine()方法获取输入的字符串，在读取前要使用 hasNext() 和 hasNextLine() 判断是否还有输入的数据**

**next()方法：**
```java
package top.cxy96.process_control;
import java.util.Scanner;
public class userScanner_next {
    public static void main(String[] args) {
        // 创建一个扫描器对象，用于接受键盘数据
        Scanner scanner=new Scanner(System.in);
        
        System.out.println("使用next接收：");
        //判断有无输入字符串
        if(scanner.hasNext()){
            String str=scanner.next();            //输入内容：hello world
            System.out.println("输出内容为："+str); //输出内容：hello
        }
        //用完关掉节省资源
        scanner.close();
    }
}
```
**nextLine()方法：**
```java
package top.cxy96.process_control;
import java.util.Scanner;
public class userScanner_nextLine {
    public static void main(String[] args) {
        // 创建一个扫描器对象，用于接受键盘数据
        Scanner scanner = new Scanner(System.in);

        System.out.println("使用nextLine接收：");
        //判断有无输入字符串
        if(scanner.hasNextLine()){
            String str= scanner.nextLine();      //输入hello world
            System.out.println("输出内容："+str); //输出hello world
        }
        //用完关掉节省资源
        scanner.close();
    }
}
```
* next() 
1. 一定要读取到有效字符后才可以结束输入
2. 对输入有效字符前遇到的空白，next()方法会自动将其去掉
3. 只有输入有效字符后才将其后面的空白作为分隔符或者结束符
4. ==next()不能得到带有空格的字符串==
* nextLine()
1. 以Enter为结束符，nextLine()方法返回的是输入回车前的所有字符
2. 可以得到空白

### 3.2 顺序结构
**java语句之间是从上到下一次执行**
```java
package top.cxy96.process_control;

public class demo1 {
    public static void main(String[] args) {
        System.out.println("hello1");
        System.out.println("hello2");
        System.out.println("hello3");
        //输出
        /*
        hello1
        hello2
        hello3
         */
    }
}
```
### 3.3 选择结构
**if 判断 基本语法：**
```java
if(判断条件1){
    执行方法1
}
else if(判断条件2){
    执行方法2
}
else{
    执行方法3
}
```
**switch 语句变量类型**
* byte、short、int、char
* Java SE7 开始支持字符串String类型
* case 必须为字符串常量或字面量

**switch判断 基本语法**
```java
switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}
```
### 3.4 循环结构
1. **while循环**   
基本语法：
```java
while(判断条件){
    //循环内容
}
```
2. **do···while循环**  
与while区别会==先执行一次==  
基本语法：
```java
do{
    //循环内容
}whiel(判断条件);
```
3. **for循环**
基本语法：
```java
for(初始化值，判断，更新语句){
    //循环内容
}
```
IDEA小tip:  ==100.for+Enter==
```java
    for (int i = 0; i < 100; i++) {
            
    }
```
4. **增强for循环（java5引入）**  
基本语法：
```java
for(声明语句 : 表达式){
    //执行语句
}
```
例：
```java
package top.cxy96.process_control;

public class 增强for循环 {
    public static void main(String[] args) {
        // 定义数组
        int[] numbers={10,20,30,40};
        // 增强for循环
        for(int x:numbers){
            System.out.println(x);
        }
    }
}
```
### 3.5 break/continue
* break:跳出循环
* continue:跳出==本次==循环
* goto:跳到指定语句(一般不用)
```java
    outer :语句
          break outer    //跳到outer的语句
          continue outer //跳到outer语句
```
