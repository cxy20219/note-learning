## 1. 线程简介

- 进程
  - 进程可以看作是程序的执行过程。一个程序的运行需要CPU时间、内存空间、文件以及I/O等资源。
  - 操作系统是以进程为单位来分配资源的，所以说进程是分配资源的基本单位。
- 线程
  - 线程是指进程中的一个执行流程，一个进程中可以运行多个线程。
  - 线程总是属于某个进程，进程中的多个线程共享进程的内存。
- 协程
  - 单线程执行任务过程中如果出现长时间的I/O操作，会出现堵塞
  - 利用协程可以在等待I/O过程中执行其他任务，待I/O完后再执行原任务
  - C#,python,go等语言支持协程操作，Java目前不支持

## 2. 线程实现

### 2.1 继承Thread实现

- 子类继承Thread类
- 启动线程:子类对象.start()

```java
package top.cxy96.multithreading.Demo01;

// 创建线程方式一：继承Thread类，重写run方法，调用start开启线程
// 线程开启不一定立即执行，由cpu调度
public class TestThread1 extends Thiixnhread{
    @Override
    public void run() {
        // run方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("run方法线程"+i);
        }
    }

    public static void main(String[] args) {
        // main 主线程

        // 创建线程对象
        TestThread1 testThread1 = new TestThread1();
        // 调用start() 开启线程
        testThread1.start();

        for (int i = 0; i < 20; i++) {
            System.out.println("main线程"+i);
        }
    }
}
```

![Demo1](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo1.png?ynotemdtimestamp=1647071903556)

#### 网图下载Demo

需要Commons IO包，下载地址：https://commons.apache.org/proper/commons-io/

```java
package top.cxy96.multithreading.Demo01;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;

// 实现多线程同步下载图片
public class TestThread2 extends Thread{
    private String url;     // url地址
    private String name;    // 文件名
    public TestThread2(String url,String name){
        this.name = name;
        this.url = url;
    }

    // 下载图片线程执行体
    @Override
    public void run() {
        WebDownLoader webDownLoader = new WebDownLoader();
        webDownLoader.downloader(url,name);
        System.out.println("下载文件名："+name);
    }

    public static void main(String[] args) {
        TestThread2 t1 = new TestThread2("https://scpic.chinaz.net/files/pic/pic9/202009/apic27858.jpg","1.jpg");
        TestThread2 t2 = new TestThread2("https://tse3-mm.cn.bing.net/th/id/OIP-C.nfC2tVNM9TgwQ5QuqECd6wHaFj?pid=ImgDet&rs=1","2.jpg");
        TestThread2 t3 = new TestThread2("https://scpic.chinaz.net/files/pic/pic9/201910/zzpic20739.jpg","3.jpg");
        t1.start();
        t2.start();
        t3.start();
    }
}
// 下载器
class WebDownLoader{
    // 下载方法
    public  void downloader(String url,String name){
        try{
            FileUtils.copyURLToFile(new URL(url),new File(name));
        }catch (IOException e){
            e.printStackTrace();
            System.out.println("IO异常，downloader出现问题");
        }
    }
}
```

结果演示：

![Demo2](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo2.png?ynotemdtimestamp=1647071903556)

### 2.2 Runnable接口实现

- 定义Runnable类实现Runnable接口
- 实现run()方法，编写执行体
- 创建线程对象，调用start()方法启动线程

代码示例：

```jav
package top.cxy96.multithreading.Demo01;

public class TestThread3 implements Runnable{
    @Override
    public void run() {
        // 线程执行体
        for (int i = 0; i < 100; i++) {
            System.out.println("run线程"+i);
        }
    }
    public static void main(String[] args) {
        // 创建Runnable接口实现类对象
        TestThread3 testThread3 = new TestThread3();
        // 创建线程对象，通过线程对象开启线程
        Thread thread = new Thread(testThread3);
        thread.start();

        for (int i = 0; i < 100; i++) {
            System.out.println("main线程"+i);
        }
    }
}
```

结果演示：

![Demo3](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo3.png?ynotemdtimestamp=1647071903556)

#### 买火车票Demo

**多线程操作同一个对象**

示例代码：

```java
package top.cxy96.multithreading.Demo01;

public class TestThread4 implements Runnable{
    // 票数
    private int ticketNums = 10;

    @Override
    public void run() {
        while (true){
            if(ticketNums <= 0){
                break;
            }
            // Thread.currentThread().getName()方法获取线程的名字
            System.out.println(Thread.currentThread().getName()+"拿到了第"+ticketNums--+"票");
        }
    }

    public static void main(String[] args) {
        TestThread4 testThread4 = new TestThread4();
        new Thread(testThread4,"张三").start();
        new Thread(testThread4,"李四").start();
        new Thread(testThread4,"王五").start();
    }
}
```

结果演示：

![Demo4](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo4.png?ynotemdtimestamp=1647071903556)

！线程不安全了，数据会出现紊乱

### 2.3 Callable接口实现

示例代码：

```java
package top.cxy96.multithreading.Demo02;

import java.util.concurrent.*;

// Callable 需要返回值
public class TestCallable implements Callable<Boolean> {
    // 票数
    private int ticketNums = 10;

    @Override
    public Boolean call(){
        while (true){
            if(ticketNums <= 0){
                break;
            }
            // Thread.currentThread().getName()方法获取线程的名字
            System.out.println(Thread.currentThread().getName()+"拿到了第"+ticketNums--+"票");
        }
        return true;
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        TestCallable t1 = new TestCallable();
        TestCallable t2 = new TestCallable();

        // 创建执行服务
        ExecutorService ser = Executors.newFixedThreadPool(2);

        // 提交执行
        Future<Boolean> result1 = ser.submit(t1);
        Future<Boolean> result2 = ser.submit(t2);

        // 获取结果
        boolean r1 = result1.get();
        boolean r2 = result2.get();

        // 关闭服务
        ser.shutdownNow();
    }
}

```

结果演示：

![Demo5](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo5.png?ynotemdtimestamp=1647071903556)

### 2.4 静态代理

* 真实对象和代理对象实现同一个接口
* 代理对象要代理真实角色
* 代理对象可以做真实对象不能做的事情

示例代码：

```java
 package top.cxy96.multithreading.Demo02;
public class StacticProxy {
    public static void main(String[] args) {
        WeddingCpmpany weddingCpmpany = new WeddingCpmpany(new You());
        weddingCpmpany.HappyMarry();
    }
}

interface Marry {
    void HappyMarry();
}
// 真实角色
class You implements Marry {
    @Override
    public void HappyMarry() {
        System.out.println("xxx结婚了");
    }
}
// 代理角色
class WeddingCpmpany implements Marry{
    private Marry target;

    public WeddingCpmpany(Marry target){
        this.target = target;
    }
    @Override
    public void HappyMarry() {
        before();
        this.target.HappyMarry();
        after();
    }

    private void before() {
        System.out.println("婚前");
    }

    private void after() {
        System.out.println("婚后");
    }
}
```

结果演示：

![Demo6](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo6.png?ynotemdtimestamp=1647071903556)

### 2.5 Lambda表达式

函数式接口：

* 任何一个接口只包含一个抽象方法，就是函数式接口
* 可以通过Lambda表达式来创建该接口的对象

示例代码：

```java
package top.cxy96.multithreading.Demo02;

public class TestLambda {
    // 3. 静态内部类
    static class Like2 implements ILike{
        @Override
        public void lambda() {
            System.out.println("This is Lambda2");
        }
    }
    public static void main(String[] args) {
        Like like = new Like();
        like.lambda();

        Like2 like2 = new Like2();
        like2.lambda();

        // 4. 局部内部类
        class Like3 implements ILike{
            @Override
            public void lambda() {
                System.out.println("This is Lambda3");
            }
        }
        Like3 like3 = new Like3();
        like3.lambda();

        // 5. 匿名内部类 ， 没有类的名字， 必须借助接口或父类
        ILike like4 = new ILike() {
            @Override
            public void lambda() {
                System.out.println("This is Lambda4");
            }
        };
        like4.lambda();

        // 6. lambda简化
        ILike like5 = ()->{System.out.println("This is Lambda5");};
        like5.lambda();
    }
}

// 1. 定义一个函数式接口
interface ILike{
    void lambda();
}
// 2. 实现类
class Like implements ILike{
    @Override
    public void lambda() {
        System.out.println("This is Lambda1");
    }
}
```

结果演示：

![Demo7](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo7.png?ynotemdtimestamp=1647071903556)

#### 传参与简化：

Lambda简化:

1. 表达式只有一行代码的情况下可以简化为一行，多行时使用代码块
2. 多个参数也可以去掉参数类型，需要加上括号

示例代码：

```java
package top.cxy96.multithreading.Demo02;

public class SimplifyLambda {
    public static void main(String[] args) {
        // 1. 直接传参
        ILove iLove1 = (int a) -> {
            System.out.println("I LOVE "+ a);
        };
        iLove1.love(520);

        // 2. 简化一：去掉参数类型
        ILove iLove2 = (a)->{
            System.out.println("I LOVE "+ a);
        };
        iLove2.love(521);

        // 3. 简化二：去掉括号
        ILove iLove3 = a->{
            System.out.println("I LOVE "+ a);
        };
        iLove3.love(522);

        // 4. 简化三：去掉大括号  
        ILove iLove4 = a-> System.out.println("I LOVE "+ a);
        iLove4.love(523);
    }
}
interface ILove{
    void love(int a);
}
```

结果演示：

![Demo8](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo8.png?ynotemdtimestamp=1647071903556)

## 3. 线程状态


```
flowchart LR
    创建状态 --> 就绪状态 --> 运行状态 ---> 就绪状态
    运行状态 --> 阻塞状态
    阻塞状态 --> 就绪状态
    运行状态 --> 结束状态
    
```  
---
**线程方法：**

  
|              方法              |            说明            |
| :----------------------------: | :------------------------: |
|  setPriority(int newPriority)  |       更改线程优先级       |
| static void sleep(long millis) |   让当前线程休眠指定毫秒   |
|          void join()           |       等待该线程终结       |
|      static void yield()       | 暂停当前线程，执行其他线程 |
|         void interript         |          中断线程          |
|       bollean isAlive()        |  测色线程是否处于活动状态  |


### 3.1 线程停止



## 4. 线程同步

## 5. 线程通信

## 6.