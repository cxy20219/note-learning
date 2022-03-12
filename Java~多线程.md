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

## 3. 线程状态

## 4. 线程同步

## 5. 线程通信

## 6.