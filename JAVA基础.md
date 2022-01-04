## 1.环境安装
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