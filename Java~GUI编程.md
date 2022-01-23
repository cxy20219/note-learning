组件:
* 窗口
* 弹窗
* 面板
* 文本框
* 列表框
* 按钮
* 图片
* 监听事件
* 鼠标
* 键盘事件
* 破解工具

## 1. 简介
GUI的核心技术：Swing、AWT
缺点：
1. 界面不美观
2. 需要jre环境

用处：
1. 可以写自己需要的小工具
2. 了解MVC架构，了解监听

## 2. AWT
### 2.1 AWT 简介
1. AWT包含很多类和接口！GUI：图形用户界面编程  
2. 元素：窗口，按钮，文本框  
3. java.awt

### 2.2 组件和容器
1. Frame
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;
public class TestFrame {
    public static void main(String[] args) {
        // Frame
        Frame frame = new Frame("Java图形界面窗口");

        // 设置可见性
        frame.setVisible(true);

        // 设置窗口大小
        frame.setSize(400,400);

        // 设置背景颜色 Color
        //frame.setBackground(Color.black);
        frame.setBackground(new Color(121, 59, 59));

        // 弹出初始位置
        frame.setLocation(200,200);

        // 设置大小固定
        frame.setResizable(false);
    }
}
```
运行结果：  
![Demo1](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo1.png)  
封装实现多个弹窗：
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;

public class TestFrame2 {
    public static void main(String[] args) {
        // 展示多个窗口
        new MyFrame(100,100,200,200,Color.BLACK);
        new MyFrame(300,100,200,200,Color.BLACK);
        new MyFrame(100,300,200,200,Color.BLACK);
        new MyFrame(300,300,200,200,Color.BLACK);
    }
}
class MyFrame extends Frame{
    static int id = 0 ;   // 计窗口数
    public MyFrame(int x,int y,int w,int h,Color color){
        super("Myframe"+(++id));
        setBackground(color);
        setBounds(x,y,w,h);
        setVisible(true);
    }
}
```
2. 面板Panel
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;

// Panel 不能单独存在
public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame();

        Panel panel = new Panel();

        // 设置布局
        frame.setLayout(null);

        // 坐标
        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(99, 229, 18));

        // panel设置坐标,相对于frame
        panel.setBounds(50,50,400,400);
        panel.setBackground(new Color(1,1,1));

        // 将面板放到窗口
        frame.add(panel);
        frame.setVisible(true);

        // 监听事件，监听窗口关闭事件  System.exit(0)
        // 适配器模式
        frame.addWindowListener(new WindowAdapter() {
            // 窗口关闭要做的事情
            @Override
            public void windowClosing(WindowEvent e) {
                // 结束程序
                System.exit(0);
            }
        });
    }
}
```  
运行结果：
![Demo1](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Java_GUI_Demo2.png)  
3. 布局管理器
* 流式布局
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;

public class TestFlow {
    public static void main(String[] args) {
        Frame frame = new Frame();

        //　组件--按钮
        Button button1=new Button("buttton1");
        Button button2=new Button("buttton2");
        Button button3=new Button("buttton3");

        // 设为流式布局
        // 默认居中
        // frame.setLayout(new FlowLayout());
        frame.setLayout(new FlowLayout(FlowLayout.LEFT));  // 居左

        frame.setSize(200,200);

        // 将按钮添加上去
        frame.add(button1);
        frame.add(button2);
        frame.add(button3);

        // 设置可见
        frame.setVisible(true);
    }
}
```  
运行结果：
![Demo3](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo3.png)
* 东西南北中
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;

public abstract class TestBorderLayout {
    public static void main(String[] args) {
        Frame frame = new  Frame("TestBorderLayout");

        Button east = new Button("East");
        Button west = new Button("West");
        Button south = new Button("South");
        Button north = new Button("North");
        Button center = new Button("Center");

        frame.add(east,BorderLayout.EAST);
        frame.add(west,BorderLayout.WEST);
        frame.add(north,BorderLayout.NORTH);
        frame.add(south,BorderLayout.SOUTH);
        frame.add(center,BorderLayout.CENTER);

        frame.setSize(200,200);
        frame.setVisible(true);
    }
}
```  
![Demo4](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo4.png)
* 表格布局
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;

public class TestGrid {
    public static void main(String[] args) {
        Frame frame = new Frame("TestGridLayout");

        Button bt1 = new Button("button1");
        Button bt2 = new Button("button2");
        Button bt3 = new Button("button3");
        Button bt4 = new Button("button4");
        Button bt5 = new Button("button5");
        Button bt6 = new Button("button6");

        frame.setLayout(new GridLayout(3,2));

        frame.add(bt1);
        frame.add(bt2);
        frame.add(bt3);
        frame.add(bt4);
        frame.add(bt5);
        frame.add(bt6);

        frame.pack(); // Java函数 自动布局
        frame.setVisible(true);

    }
}
```  
运行结果： 
![Demo5](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo5.png)
 
## 3. Swing