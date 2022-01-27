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
 
 
### 综合案列
效果展示：  
![Demo6](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo6.png)  
代码：  
```java
package top.cxy96.java_GUI.lesson1;

import java.awt.*;

public class Demo {
    public static void main(String[] args) {
        // 大的窗口
        Frame frame = new Frame();
        // 两行一列
        frame.setLayout(new GridLayout(2,1));
        // 设置大小
        frame.setSize(400,300);
        // 设置位置
        frame.setLocation(300,400);
        // 设置背景颜色
        frame.setBackground(Color.black);
        // 设置可见
        frame.setVisible(true);

        // 4个面板
        Panel p1 = new Panel(new BorderLayout());
        Panel p2 = new Panel(new GridLayout(2,1));
        Panel p3 = new Panel(new BorderLayout());
        Panel p4 = new Panel(new GridLayout(2,2));

        // 按钮
        p1.add(new Button("East-1"),BorderLayout.EAST);
        p1.add(new Button("West-1"),BorderLayout.WEST);
        p2.add(new Button("p2-btn-1"));
        p2.add(new Button("p2-btn-2"));

        // 将表格布局放在中间
        p1.add(p2,BorderLayout.CENTER);

        // 按钮
        p3.add(new Button("East-2"),BorderLayout.EAST);
        p3.add(new Button("West-2"),BorderLayout.WEST);
        for (int i = 0; i < 4; i++) {
            p4.add(new Button("p4-btn-"+i));
        }

        // 将表格布局放在中间
        p1.add(p2,BorderLayout.CENTER);
        p3.add(p4,BorderLayout.CENTER);

        // 将面板放在frame里面
        frame.add(p1);
        frame.add(p3);
    }
}
```
## 3. 事件监听
### 3.1 按钮监听事件
代码：  
```java
package top.cxy96.java_GUI.lesson2;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestAction {
    public static void main(String[] args) {
        // 按下按钮发生事件
        Frame frame = new Frame();
        Button button = new Button("clik");

        // 构造一个ActionListener
        MyActionListener myActionListener = new MyActionListener();

        button.addActionListener(myActionListener);

        frame.add(button,BorderLayout.CENTER);

        frame.pack();
        frame.setVisible(true);

        // 关闭窗口
        windowColse(frame);
    }
    // 关闭窗体事件
    private static void windowColse(Frame frame){
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}
class MyActionListener implements ActionListener{
    @Override
    public void actionPerformed(ActionEvent e) {
        // 点击按钮时打印aaa
        System.out.println("aaa");
        // 获取按钮上的信息
        System.out.println("按钮："+e.getActionCommand());
    }
}
```

### 3.2. 输入框监听事件
代码：
```java
package top.cxy96.java_GUI.lesson2;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class TestText01 {
    public static void main(String[] args) {
        MyFrame myFrame = new MyFrame();
    }
}
class MyFrame extends Frame{
    public MyFrame(){
        TextField textField = new TextField();
        add(textField);

        // 监听文本框输入的文字
        MyActionListener2 myActionListener2 = new MyActionListener2();
        // 按下Enter触发事件
        textField.addActionListener(myActionListener2);

        // 设置替换编码
        textField.setEchoChar('*');
        setVisible(true);
        pack();

    }
}

class MyActionListener2 implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent e) {
        // 获得一些资源 , 返回一个对象 ，强转TextField
        TextField field = (TextField)e.getSource();
        String messge = field.getText();   // 获取输入框的文本
        System.out.println(messge);

        // 清空输入框的文本
        field.setText(null);  // "" 或 null
    }
}
```  
### 3.3 简易计算器
#### 实现代码
```java
package top.cxy96.java_GUI.lesson2;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleCalculator {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
    }
}
// 计算器类
class Calculator extends Frame{
    public Calculator(){
        // 3个文本框
        TextField textField1 = new TextField(10); // 字符数
        TextField textField2 = new TextField(10); // 字符数
        TextField textField3 = new TextField(20); // 字符数
        
        // 1个按钮
        Button button = new Button("=");

        button.addActionListener(new MyCalculatorListener(textField1,textField2,textField3));
        // 一个标签
        Label label = new Label("+");

        // 布局
        setLayout(new FlowLayout());

        add(textField1);
        add(label);
        add(textField2);
        add(button);
        add(textField3);
        
        pack();
        setVisible(true);
    }
}
// 监听器类
class MyCalculatorListener implements ActionListener{
    // 获取三个变量
    private TextField num1,num2,num3;
    public MyCalculatorListener(TextField num1,TextField num2,TextField num3){
        this.num1 = num1;
        this.num2 = num2;
        this.num3 = num3;
    }
    @Override
    public void actionPerformed(ActionEvent e) {
        // 获得加数与被加数
        int n1 = Integer.parseInt(num1.getText());
        int n2 = Integer.parseInt(num2.getText());

        // 将运算后的值放到第三个框
        num3.setText(""+(n1+n2));

        // 清除前两个框
        num1.setText(null);
        num2.setText(null);
    }
}
```
结果演示：
![Demo7](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo7.png)  
![Demo8](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo8.png)  

#### 代码优化(组合类)
```java
package top.cxy96.java_GUI.lesson2;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleCalculator {
    public static void main(String[] args) {
        new Calculator().loadFrame();
    }
}
// 计算器类
class Calculator extends Frame{
    // 属性
    TextField textField1,textField2,textField3;

    // 方法
    public void loadFrame() {
        // 3个文本框
        textField1 = new TextField(10); // 字符数
        textField2 = new TextField(10); // 字符数
        textField3 = new TextField(20); // 字符数

        // 1个按钮
        Button button = new Button("=");

        button.addActionListener(new MyCalculatorListener(this));
        // 一个标签
        Label label = new Label("+");

        // 布局
        setLayout(new FlowLayout());

        add(textField1);
        add(label);
        add(textField2);
        add(button);
        add(textField3);

        pack();
        setVisible(true);
    }
}
// 监听器类
class MyCalculatorListener implements ActionListener{
    // 获取计算器对象  在一个类中组合另一个类
    Calculator calculator = null;
    public MyCalculatorListener(Calculator calculator){
        this.calculator = calculator;
    }
    @Override
    public void actionPerformed(ActionEvent e) {
        // 获得加数与被加数
        int n1 = Integer.parseInt(calculator.textField1.getText());
        int n2 = Integer.parseInt(calculator.textField2.getText());

        // 将运算后的值放到第三个框
        calculator.textField3.setText(""+(n1+n2));

        // 清除前两个框
        calculator.textField1.setText(null);
        calculator.textField2.setText(null);
    }
}
```
#### 代码优化(类部类)
```java
package top.cxy96.java_GUI.lesson2;

import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleCalculator {
    public static void main(String[] args) {
        new Calculator().loadFrame();
    }
}
// 计算器类
class Calculator extends Frame{
    // 属性
    TextField textField1,textField2,textField3;

    // 方法
    public void loadFrame() {
        // 3个文本框
        textField1 = new TextField(10); // 字符数
        textField2 = new TextField(10); // 字符数
        textField3 = new TextField(20); // 字符数

        // 1个按钮
        Button button = new Button("=");

        button.addActionListener(new MyCalculatorListener());
        // 一个标签
        Label label = new Label("+");

        // 布局
        setLayout(new FlowLayout());

        add(textField1);
        add(label);
        add(textField2);
        add(button);
        add(textField3);

        pack();
        setVisible(true);
    }
    // 监听器类
    private class MyCalculatorListener implements ActionListener{
        @Override
        public void actionPerformed(ActionEvent e) {
            // 获得加数与被加数
            int n1 = Integer.parseInt(textField1.getText());
            int n2 = Integer.parseInt(textField2.getText());

            // 将运算后的值放到第三个框
            textField3.setText(""+(n1+n2));

            // 清除前两个框
            textField1.setText(null);
            textField2.setText(null);
        }
    }
}
```