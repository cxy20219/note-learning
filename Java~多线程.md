## 1. 线程简介

* 进程

  * 进程可以看作是程序的执行过程。一个程序的运行需要CPU时间、内存空间、文件以及I/O等资源。
  * 操作系统是以进程为单位来分配资源的，所以说进程是分配资源的基本单位。

* 线程

  * 线程是指进程中的一个执行流程，一个进程中可以运行多个线程。

  * 线程总是属于某个进程，进程中的多个线程共享进程的内存。

* 协程

  * 单线程执行任务过程中如果出现长时间的I/O操作，会出现堵塞
  * 利用协程可以在等待I/O过程中执行其他任务，待I/O完后再执行原任务
  * C#,python,go等语言支持协程操作，Java目前不支持

## 2. 线程实现

1. 继承Thread实现

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

   ![Demo1](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo1.png)

   

2. 

## 3. 线程状态
## 4. 线程同步
## 5. 线程通信
## 6. 