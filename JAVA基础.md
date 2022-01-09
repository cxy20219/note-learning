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

## 2. 基本语法

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
