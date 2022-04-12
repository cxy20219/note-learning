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

![Demo10](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo10.png?ynotemdtimestamp=1647071903556)

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
1. 建议线程正常停止------ 利用次数，不建议死循环
2. 建议使用标志位 ------ 设置一个标志位
3. 不要使用stop或者destory (JDK不建议使用)

示例代码：

```java
package top.cxy96.multithreading.Demo03;

// 测试stop
public class TestStop implements Runnable {
    // 1. 设置一个标志位
    private boolean flag = true;
    @Override
    public void run() {
        int i=0;
        while (flag){
            System.out.println("runing"+i++);
        }
    }

    // 2. 设置一个方法停止线程，转换标志位
    public void stop(){
        this.flag = false;
    }
    public static void main(String[] args) {
        TestStop testStop = new TestStop();
        new Thread(testStop,"test").start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if (i == 900) {
                testStop.stop();
                System.out.println("线程该停止了!");
            }
        }
    }
}
```

结果演示：

![Demo9](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo9.png?ynotemdtimestamp=1647071903556)

### 3.2 线程休眠

* 指定当前线程阻塞的毫秒数
* 存在interruptedException异常
* sleep时间后线程进入就绪状态
* sleep不会释放锁

示例代码：

```java
package top.cxy96.multithreading.Demo03;

public class TestSleep {
    public static void main(String[] args) {
        try {
            new delayTime(15).tenDowm();
        }
        catch (InterruptedException e){
            e.printStackTrace();
        }
    }

}
// 模拟倒计时
class delayTime{
    private static int num;

    delayTime(int num){
        this.num = num;
    }
    static void tenDowm() throws InterruptedException {
        while (true){
            Thread.sleep(1000);
            System.out.println(num--);
            if (num<=0){
                break;
            }
        }
    }
}

```

结果演示：

![Demo11](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo11.png?ynotemdtimestamp=1647071903556)

### 3.3 线程礼让

* 让当前正在执行的线程暂停，不阻塞
* 将线程从运行状态转为就绪状态
* ！ 礼让不一定成功

示例代码：

```java
package top.cxy96.multithreading.Demo03;

public class TestYield {
    public static void main(String[] args) {
        MyYield myYield = new MyYield();
        new Thread(myYield,"a").start();
        new Thread(myYield,"b").start();
    }
}
class MyYield implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"线程开始执行");
        Thread.yield();
        System.out.println(Thread.currentThread().getName()+"线程停止执行");
    }
}

```

结果演示：

![Demo12](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo12.png?ynotemdtimestamp=1647071903556)

![Demo13](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo13.png?ynotemdtimestamp=1647071903556)

### 3.4 线程强制执行

* Join 合并线程，待线程执行完成后，再执行其他线程，其他线程阻塞

示例代码：

```java
package top.cxy96.multithreading.Demo03;

public class TestJoin {
    public static void main(String[] args) {
        MyProcess myProcess = new MyProcess();
        Thread thread = new Thread(myProcess,"Vip");
        thread.start();
        for (int i = 0; i < 500; i++) {
            if (i==100){
                try {
                    thread.join(); // 强制执行
                }
                catch (InterruptedException e){
                    e.printStackTrace();
                }
            }
            System.out.println("main线程"+i);
        }

    }
}
class MyProcess implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("线程Vip来了"+i);
        }
    }
}
```

结果演示：

![Demo14](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo14.png?ynotemdtimestamp=1647071903556)

### 3.5 观察线程状态

线程状态。 线程可以处于以下状态之一：

- [`NEW`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#NEW)
  尚未启动的线程处于此状态。
- [`RUNNABLE`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#RUNNABLE)
  在Java虚拟机中执行的线程处于此状态。
- [`BLOCKED`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#BLOCKED)
  被阻塞等待监视器锁定的线程处于此状态。
- [`WAITING`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#WAITING)
  正在等待另一个线程执行特定动作的线程处于此状态。
- [`TIMED_WAITING`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#TIMED_WAITING)
  正在等待另一个线程执行动作达到指定等待时间的线程处于此状态。
- [`TERMINATED`](https://www.matools.com/file/manual/jdk_api_1.8_google/java/lang/Thread.State.html#TERMINATED)
  已退出的线程处于此状态。

实例代码：

```java
package top.cxy96.multithreading.Demo03;

public class TestState {
    public static void main(String[] args) {
        Thread thread = new Thread(()->{
            for (int i = 0; i < 5; i++) {
                try{
                    Thread.sleep(10);
                }
                catch (InterruptedException e){
                    e.printStackTrace();
                }
            }
        }
        );

        // 观察状态
        Thread.State state = thread.getState();
        System.out.println(state);

        // 启动线程
        thread.start();
        state = thread.getState();
        System.out.println(state);

        while (state != Thread.State.TERMINATED){
            state = thread.getState();
            System.out.println(state);
        }
    }
}
```

结果演示：

![Demo15](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo15.png?ynotemdtimestamp=1647071903556)

### 3.6 线程优先级

* Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程
* 线程优先级数字表示 1 ~ 10
* 使用getPriority()获取优先级
* 使用setPriority()设置优先级

实例代码：

```java
package top.cxy96.multithreading.Demo03;

public class TestPriority{
    public static void main(String[] args) {
        MyPriority myPriority = new MyPriority();

        Thread a = new Thread(myPriority,"a");
        Thread b = new Thread(myPriority,"b");
        Thread c = new Thread(myPriority,"c");
        Thread d = new Thread(myPriority,"d");

        // 设置优先级
        a.start();
        b.setPriority(1);
        b.start();
        c.setPriority(4);
        c.start();
        d.setPriority(Thread.MAX_PRIORITY);
        d.start();
        // 主线程 默认优先级
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
    }
}
class MyPriority implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
    }
}

```

结果演示：

![Demo16](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo16.png?ynotemdtimestamp=1647071903556)

### 3.7 守护线程

* 用户线程结束则守护线程结束

```java
package top.cxy96.multithreading.Demo03;

public class TestDaemon {
    public static void main(String[] args) {
        God god = new God();
        Thread thread = new Thread(god);
        thread.setDaemon(true);   // 默认为false用户线程
        thread.start();

        Person you = new Person();
        new Thread(you).start();
    }
}
class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("三清老祖保佑你！");
        }
    }
}

class Person implements Runnable{
    @Override
    public void run() {
        System.out.println("hello world!");
        for (int i = 0; i < 36500; i++) {
            System.out.println("开心地敲代码");
        }
        System.out.println("good bye world!");
    }
}
```



## 4. 线程同步

### 4.1 线程同步机制

线程锁：

* 一个线程锁上时其他线程需等待
* 会引起性能问题
* 如果优先级高的线程等优先级低的线程释放锁，会导致优先级倒置，引起性能问题

### 4.2 线程安全

**不安全示例1：**

```jav
package top.cxy96.multithreading.Demo04;

public class UnsafeBuyTicket {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();
        new Thread(buyTicket,"小明").start();
        new Thread(buyTicket,"黄牛").start();
        new Thread(buyTicket,"小强").start();
    }
}
class BuyTicket implements Runnable{
    private int tickNums = 10;    // 票
    boolean flag = true; // 外部停止标志
    @Override
    public void run() {
        while (flag){
            try{
                buy();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
    }

    private void buy() throws InterruptedException{
        if(tickNums<=0){
            flag = false;
            return;
        }
        // 模拟延时
        Thread.sleep(100);
        // 买票
        System.out.println(Thread.currentThread().getName()+"拿到"+tickNums--);
    }
}
```

结果演示：

![Demo17](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo17.png?ynotemdtimestamp=1647071903556)

**不安全案列2：**

```java
package top.cxy96.multithreading.Demo04;

public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account("张三",1_000_000);
        Drawing zhangsan = new Drawing(account,600_000,"张三");
        Drawing girlfriend = new Drawing(account,500_000,"girlfriend");
        zhangsan.start();
        girlfriend.start();
    }
}

// 账户
class Account{
    int money;
    String name;
    public Account(String name,int money) {
        this.name = name;
        this.money = money;
    }
}
// 银行
class Drawing extends Thread{
    Account account;
    int drawingMoney;
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);
        this.drawingMoney = drawingMoney;
        this.account = account;
    }

    @Override
    public void run() {
        if(account.money - drawingMoney<0){
            System.out.println(Thread.currentThread().getName()+"余额不足");
            return;
        }

        try{
            Thread.sleep(1000);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        account.money = account.money-drawingMoney;
        nowMoney = nowMoney+drawingMoney;
        System.out.println(account.name+"余额："+account.money);
        System.out.println(this.getName()+"现金"+nowMoney);
    }
}
```

结果演示：

![Demo18](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo18.png?ynotemdtimestamp=1647071903556)

**不安全案例3：**

```java
package top.cxy96.multithreading.Demo04;

import java.util.ArrayList;
import java.util.List;

public class UnsafeList {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());
            }).start();
        }
        System.out.println(list.size());
    }
}
```

结果演示：

![Demo19](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo19.png?ynotemdtimestamp=1647071903556)

### 4.3 同步方法

用synchronized为对象加上一把锁。

**案例1同步实现：**

```java
package top.cxy96.multithreading.Demo04;

public class UnsafeBuyTicket {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();
        new Thread(buyTicket,"小明").start();
        new Thread(buyTicket,"黄牛").start();
        new Thread(buyTicket,"小强").start();
    }
}
class BuyTicket implements Runnable{
    private int tickNums = 10;    // 票
    boolean flag = true; // 外部停止标志
    @Override
    public void run() {
        while (flag){
            try{
                buy();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
    }
    // synchronized 同步方法,锁this
    private synchronized void buy() throws InterruptedException{
        if(tickNums<=0){
            flag = false;
            return;
        }
        // 模拟延时
        Thread.sleep(100);
        // 买票
        System.out.println(Thread.currentThread().getName()+"拿到"+tickNums--);
    }
}
```

结果演示：

![Demo20](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo20.png?ynotemdtimestamp=1647071903556)

**案例2同步实现：**

```java
package top.cxy96.multithreading.Demo04;

public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account("张三",1_000_000);
        Drawing zhangsan = new Drawing(account,600_000,"张三");
        Drawing girlfriend = new Drawing(account,500_000,"girlfriend");
        zhangsan.start();
        girlfriend.start();
    }
}

// 账户
class Account{
    int money;
    String name;
    public Account(String name,int money) {
        this.name = name;
        this.money = money;
    }
}
// 银行
class Drawing extends Thread{
    Account account;
    int drawingMoney;
    int nowMoney;

    public Drawing(Account account,int drawingMoney,String name){
        super(name);
        this.drawingMoney = drawingMoney;
        this.account = account;
    }

    @Override
    public void run() {
        // 锁要变化的对象
        synchronized ((account)) {
            if (account.money - drawingMoney < 0) {
                System.out.println(Thread.currentThread().getName() + "余额不足");
                return;
            }

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            account.money = account.money - drawingMoney;
            nowMoney = nowMoney + drawingMoney;
            System.out.println(account.name + "余额：" + account.money);
            System.out.println(this.getName() + "现金" + nowMoney);
        }
    }
}
```

结果演示：

![Demo21](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo21.png?ynotemdtimestamp=1647071903556)

**案例3同步实现：**

```ja
package top.cxy96.multithreading.Demo04;

import java.util.ArrayList;
import java.util.List;

public class UnsafeList {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                synchronized (list) {
                    list.add(Thread.currentThread().getName());
                }
            }).start();
        }
        try {
            Thread.sleep(100);
        }
        catch (InterruptedException e){
            e.printStackTrace();
        }
        System.out.println(list.size());
    }
}
```

结果演示：

![Demo22](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo22.png?ynotemdtimestamp=1647071903556)

**安全的列表：**

```jave
package top.cxy96.multithreading.Demo04;

import java.util.concurrent.CopyOnWriteArrayList;

public class TestJUC {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());
            }).start();
        }
        try{
            Thread.sleep(100);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        System.out.println(list.size());
    }
}
```

结果演示：

![Demo22](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo22.png?ynotemdtimestamp=1647071903556)

### 4.4 死锁

​	多个线程各自占有一些共享资源，并且相互等待其他线程占有的资源才能运行，而导致两个或多个线程都在等待对方释放资源，都停止执行的情况。

**死锁产生情况：**

* 一个资源每次只能被一个进程使用
* 一个进程请求资源阻塞时，对以获取资源保存锁的状态

实列代码：

```java
package top.cxy96.multithreading.Demo04;

public class DeadLock {
    public static void main(String[] args) {
        Eat eat1 = new Eat(0, "张三");
        Eat eat2 = new Eat(1, "李四");
        eat1.start();
        eat2.start();
    }
}
// 鸡腿
class ChiekenLeg{}
// 苹果
class Apple{}
class Eat extends Thread{
    // 需要的资源只有一份 ，用static来保证只有一份
    static ChiekenLeg chiekenleg = new ChiekenLeg();
    static Apple apple = new Apple();
    int choice;
    String PersonName; // 吃东西的人

    Eat(int choice,String name){
        this.choice = choice;
        this.PersonName = name;
    }

    @Override
    public void run() {
        try{
            eat();
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
    private void eat() throws InterruptedException{
        if(choice==0){
            synchronized (chiekenleg){
                System.out.println(this.PersonName+"获取鸡腿的锁");
                Thread.sleep(1000);
                synchronized (apple){
                    System.out.println(this.PersonName+"获取苹果的锁");
                }
            }
        }else{
            synchronized (apple){
                System.out.println(this.PersonName+"获取苹果的锁");
                Thread.sleep(1000);
                synchronized (chiekenleg){
                    System.out.println(this.PersonName+"获取鸡腿的锁");
                }
            }
        }
    }
}
```



结果演示：

![Demo23](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo23.png?ynotemdtimestamp=1647071903556)

防止死锁：

```java
package top.cxy96.multithreading.Demo04;

public class DeadLock {
    public static void main(String[] args) {
        Eat eat1 = new Eat(0, "张三");
        Eat eat2 = new Eat(1, "李四");
        eat1.start();
        eat2.start();
    }
}
// 鸡腿
class ChiekenLeg{}
// 苹果
class Apple{}
class Eat extends Thread{
    // 需要的资源只有一份 ，用static来保证只有一份
    static ChiekenLeg chiekenleg = new ChiekenLeg();
    static Apple apple = new Apple();
    int choice;
    String PersonName; // 吃东西的人

    Eat(int choice,String name){
        this.choice = choice;
        this.PersonName = name;
    }

    @Override
    public void run() {
        try{
            eat();
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
    private void eat() throws InterruptedException{
        if(choice==0){
            synchronized (chiekenleg){
                System.out.println(this.PersonName+"获取鸡腿的锁");
                Thread.sleep(1000);
            }
            synchronized (apple){
                System.out.println(this.PersonName+"获取苹果的锁");
            }
        }else{
            synchronized (apple){
                System.out.println(this.PersonName+"获取苹果的锁");
                Thread.sleep(1000);
            }
            synchronized (chiekenleg){
                System.out.println(this.PersonName+"获取鸡腿的锁");
            }
        }
    }
}
```

### 4.5 Lock

* JDK5.0开始通过显式定义同步锁对象来实现同步
* java.util.concurrentlocks.Lock接口是控制多个线程对共享资源进行访问的工具。
* ReentrantLock类实现Lock,拥有与synchronized相同的并发性。

示例代码：

```java
package top.cxy96.multithreading.Demo04;

import java.util.concurrent.locks.ReentrantLock;

public class TestLock {
    public static void main(String[] args) {
        TestLock2 testLock2 = new TestLock2();
        new Thread(testLock2).start();
        new Thread(testLock2).start();
        new Thread(testLock2).start();
    }
}
class TestLock2 implements Runnable{
    int ticketNums = 10;

    // 定义Lock锁
    private final ReentrantLock lock = new ReentrantLock();

    @Override
    public void run() {
        while (true){
            lock.lock();                // 加锁
            try{
                if(ticketNums>0){
                    try{
                        Thread.sleep(1000);
                    }catch (InterruptedException e){
                        e.printStackTrace();
                    }
                    System.out.println(ticketNums--);
                }else{
                    break;
                }
            }finally {
                lock.unlock();          // 解锁
            }
        }
    }
}
```

结果演示：

![Demo24](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo24.png?ynotemdtimestamp=1647071903556)

## 5. 线程通信

### 5.1 生产者消费者问题

![Demo25](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo25.png?ynotemdtimestamp=1647071903556)

#### 管程法：

示例代码：

```java
package top.cxy96.multithreading.Demo05;

// 测试生产者消费者模式-->利用缓冲区解决：管程法
public class TestPC {
    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Productor(container).start();
        new Consumer(container).start();
    }
}
// 生产者
class Productor extends Thread{
    SynContainer container;
    public Productor(SynContainer container){
        this.container = container;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.push(new Chicken(i));
            System.out.println("生产了"+i+"只鸡");
        }
    }
}

// 消费者
class Consumer extends Thread{
    SynContainer container;
    public Consumer(SynContainer container){
        this.container = container;
    }
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了-->"+container.pop().id+"只鸡");
        }
    }
}

// 产品
class Chicken{
    int id;  // 产品编号
    public Chicken(int id) {
        this.id = id;
    }
}

// 缓冲区
class SynContainer{
    // 容器大小
    Chicken[] chickens = new Chicken[10];
    // 容器计数器
    int count = 0;

    // 生产者放入产品
    public synchronized void push(Chicken chicken){
        if(count == chickens.length){
            // 通知消费者消费,生产者等待
            try{
                this.wait();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        chickens[count] = chicken;
        // 同志消费者
        this.notify();
        count++;
    }

    // 消费者消费产品
    public synchronized Chicken pop(){
        if(count==0){
            // 等待生产者生产。消费者等待
            try{
                this.wait();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        count--;
        Chicken chicken = chickens[count];
        // 通知生产者
        this.notify();
        return chicken;
    }
}
```

结果演示：

![Demo26](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo26.png?ynotemdtimestamp=1647071903556)


#### 信号灯法：

示例代码：

```java
package top.cxy96.multithreading.Demo05;

// 信号灯法：标志位解决
public class TestPC2 {
    public static void main(String[] args) {
        Food food = new Food();
        new Restaurant(food).start();
        new Customer(food).start();

    }
}
// 生产者
class Restaurant extends Thread{
    Food food = new Food();
    public Restaurant(Food food) {
        this.food = food;
    }
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            if(i%2 == 0){
                this.food.product("鱼香肉丝");
            }
            else {
                this.food.product("肉末茄子");
            }
        }
    }
}
// 消费者
class Customer extends Thread{
    Food food = new Food();

    public Customer(Food food) {
        this.food = food;
    }
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            this.food.eat();
        }
    }
}
// 产品
class Food{
    String foodName;
    boolean flag = true;
    // 做饭
    public synchronized void product(String foodName){
        System.out.println("做了"+foodName);
        // 通知顾客吃饭
        if(!flag) {
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.foodName = foodName;
        this.notifyAll();
        this.flag = !this.flag;
    }
    // 吃饭
    public synchronized void eat(){
        if(flag){
            try {
                this.wait();
            }catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("吃了"+foodName);
        // 通知饭馆做饭
        this.notifyAll();
        this.flag = !this.flag;
    }
}
```

结果演示：

![Demo27](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo27.png?ynotemdtimestamp=1647071903556)

### 5.2 线程池

好处：

* 把创建的线程放入线程池，节省了线程创建和销毁的资源消耗
* 便于线程管理

使用：

* JDK5.0起提供了线程池相关的API:ExecutorService 和 Executors

示例代码：

```java
package top.cxy96.multithreading.Demo05;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class TestPool {
    public static void main(String[] args) {
        // 创建线程池
        ExecutorService executorService =  Executors.newFixedThreadPool(10);

        // 将线程放进线程池
        for (int i = 0; i < 11; i++) {
            executorService.execute(new MyThread());
        }

        // 关闭连接
        executorService.shutdownNow();
    }
}

class MyThread implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}
```

结果演示：

![Demo28](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Multithreading_Demo28.png?ynotemdtimestamp=1647071903556)

