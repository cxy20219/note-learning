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
### 3.4 画笔
代码：  
```java
package top.cxy96.java_GUI.lesson3;

import java.awt.*;

public class TestPaint {
    public static void main(String[] args) {
        new MyPaint().loadFrame();
    }
}
class MyPaint extends Frame{
    public void loadFrame(){
        setBounds(200,200,600,500);
        setVisible(true);
    }
    // 画笔
    @Override
    public void paint(Graphics g) {
        // super.paint(g);
        // 画笔颜色
        g.setColor(Color.red);

        // 画
        g.drawOval(100,100,100,100); // 圆

        g.fillOval(200,200,100,100); // 实心圆

        g.setColor(Color.green);
        g.fillRect(100,300,100,100); // 矩形
        
        // 画笔用完还原到最初颜色
        
    }
}
```  
结果演示：  
![Demo9](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo9.png)  

### 3.5 鼠标监听
代码：  
```java
package top.cxy96.java_GUI.lesson3;

import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.ArrayList;
import java.util.Iterator;

public class TestMouseListener {
    public static void main(String[] args) {
        new MyFrame("画画");
    }
}

class MyFrame extends Frame{
    // 画画需要画笔，首先监听当前的位置，需要集合来存储这个点
    ArrayList points;
    public MyFrame(String title){
        super(title);
        setBounds(200,200,600,500);

        // 存储鼠标点击的点
        points = new ArrayList<>();
        // 鼠标监听器
        this.addMouseListener(new MyMouseListener());

        setVisible(true);
    }

    @Override
    public void paint(Graphics g) {
        // 画画监听鼠标的事件
        Iterator iterator = points.iterator();
        while (iterator.hasNext()){
            Point point = (Point) iterator.next();
            g.setColor(Color.red);
            g.fillOval(point.x,point.y,10,10);
        }
    }

    // 添加一个点在界面上
    public void addPoint(Point point){
        points.add(point);
    }
    // 适配器模式
    private  class MyMouseListener extends MouseAdapter {
        // 鼠标 按下，弹起，按住不放
        @Override
        public void mousePressed(MouseEvent e) {
            MyFrame myFrame = (MyFrame) e.getSource();

            myFrame.addPoint(new Point(e.getX(),e.getY()));

            // 每次点击都需要重新画一遍
            myFrame.repaint(); // 刷新
        }
    }
}
```
结果演示：  
![Demo10](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo10.png)  

### 3.6 窗口监听
```java
package top.cxy96.java_GUI.lesson3;

import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestWindow {
    public static void main(String[] args) {
        new WindowFrame();
    }
}

class WindowFrame extends Frame{
    public WindowFrame(){
        setBounds(200,200,600,500);
        setVisible(true);
        // addWindowListener(new MyWindowListener());
        addWindowListener(
                // 匿名内部类
                new WindowAdapter() {
                    @Override
                    public void windowOpened(WindowEvent e) {
                        System.out.println("窗口打开");
                    }

                    @Override
                    public void windowActivated(WindowEvent e) {
                        System.out.println("窗口激活");
                    }

                    @Override
                    public void windowClosing(WindowEvent e) {
                        System.out.println("你点击了×");
                    }
                }
        );
    }
    class MyWindowListener extends WindowAdapter{
        @Override
        public void windowClosing(WindowEvent e) {
            setVisible(false);  // 隐藏窗口
            System.exit(0);  // 正常退出
        }
    }
}
```
### 3.7 键盘监听
```java
package top.cxy96.java_GUI.lesson3;

import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;

public class TestKeyLisenser {
    public static void main(String[] args) {
        new KeyFrame();
    }
}
class KeyFrame extends Frame{
    public KeyFrame(){
        setBounds(200,200,600,500);
        setVisible(true);

        addKeyListener(new KeyAdapter() {
            // 键盘按下
            @Override
            public void keyPressed(KeyEvent e) {
                // 获取键盘的码
                int keyCode = e.getKeyCode();
                System.out.println(keyCode);
                if(keyCode == KeyEvent.VK_UP){
                    System.out.println("按下上键");
                }
            }
        });
    }
}
```

## 4. Swing

### 4.1 窗口、面板
代码：  
```java
package top.cxy96.java_GUI.lesson4;

import javax.swing.*;

public class JFrameDemo {
    //init() 初始化
    public void init(){
        // 顶级窗口
        JFrame frame = new JFrame("这是一个JFrame窗口");
        frame.setVisible(true);
        frame.setBounds(100,100,200,200);

        // 设置文字 JLabel
        JLabel jLabel = new JLabel("Java学习");
        frame.add(jLabel);

        // 容器实例化


        // 关闭事件
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
    public static void main(String[] args) {
        // 建立一个窗口
        new JFrameDemo().init();

    }
}
```
结果：  
![Demo11](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo11.png)

==让文字居中==  
代码：  
```java
package top.cxy96.java_GUI.lesson4;

import javax.swing.*;
import java.awt.*;

public class JFrameDemo2 {
    public static void main(String[] args) {
        new MyFrame().init();
    }
}
class MyFrame extends JFrame{
    public void init(){
        this.setBounds(10,10,200,300);
        this.setVisible(true);
        JLabel jLabel = new JLabel("JavaGUI学习");
        this.add(jLabel);

        // 让文本标签居中 设置水平对齐
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);

        // 获得一个容器
        Container contentPane = this.getContentPane();
        contentPane.setBackground(Color.BLUE);

    }
}
```
结果：   
![Demo12](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo12.png)

### 4.2 弹窗
```java
package top.cxy96.java_GUI.lesson4;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class DialogDemo extends JFrame {
    public DialogDemo(){
        this.setVisible(true);
        this.setSize(700,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

        // JFrame 容器
        Container container = this.getContentPane();
        // 绝对布局
        container.setLayout(null);

        // 按钮
        JButton jButton = new JButton("点击弹出对话窗");
        jButton.setBounds(30,30,200,50);

        // 点击按钮时，弹出弹窗
        jButton.addActionListener(new ActionListener() {
            //　监听器
            @Override
            public void actionPerformed(ActionEvent e) {
                // 弹窗
                new MyDialogDemo();
            }
        });
        container.add(jButton);
    }
    public static void main(String[] args) {
        new DialogDemo();
    }
}
// 弹窗窗口
class MyDialogDemo extends JDialog{
    public MyDialogDemo() {
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        // this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);  // 默认有关闭事件

        Container contentPane = this.getContentPane();
        contentPane.setLayout(null);

        contentPane.add(new Label("hello"));
    }
}
```  

### 4.3 标签

label

```java
new JLabel("xxx");
```

图标 ICON

```java
package top.cxy96.java_GUI.lesson5;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class ImageIconDemo extends JFrame {
    public ImageIconDemo(){
        // 获取图片地址
        JLabel label = new JLabel("ImageIcon");
        // 同级目录下
        URL url = ImageIconDemo.class.getResource("man.jpg");
        ImageIcon imageIcon = new ImageIcon(url);
        label.setIcon(imageIcon);
        label.setHorizontalAlignment(SwingConstants.CENTER);

        Container contentPane = getContentPane();
        contentPane.add(label);
        setVisible(true);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        setBounds(100,100,200,200);
    }
    public static void main(String[] args) {
        new ImageIconDemo();
    }
}
```

### 4.4 面板

Panel  

```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;

public class Jpanel extends JFrame {
    public Jpanel(){
        Container contentPane = this.getContentPane();
        contentPane.setLayout(new GridLayout(2,1,10,10)); // 后面参数间距
        JPanel jPanel = new JPanel(new GridLayout(1,3));
        jPanel.add(new JButton("1"));
        jPanel.add(new JButton("2"));
        jPanel.add(new JButton("3"));
        contentPane.add(jPanel);
        this.setVisible(true);
        this.setSize(500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new Jpanel();
    }
}
```  

结果：  
![Demo13](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo13.png)

JScrollPanel
```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;

public class JScrollDemoDemo extends JFrame {
    public JScrollDemoDemo() {
        Container contentPane = this.getContentPane();

        // 文本域
        JTextArea jTextArea = new JTextArea(20,50);
        jTextArea.setText("学Java认识Java");
        contentPane.add(jTextArea);

        // Scroll面板
        JScrollPane jScrollPane = new JScrollPane(jTextArea);
        contentPane.add(jScrollPane);


        this.setVisible(true);
        this.setBounds(100,100,300,350);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JScrollDemoDemo();
    }
}
```
结果：  
![Demo14](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo14.png)

### 4,5 按钮
图片按钮  
```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo01 extends JFrame {
    public JButtonDemo01(){
        Container contentPane = this.getContentPane();
        URL url = JButtonDemo01.class.getResource("man.jpg");
        // 将图片变为图标
        ImageIcon imageIcon = new ImageIcon(url);

        // 把图标放在按钮上
        JButton jButton = new JButton();
        jButton.setIcon(imageIcon);
        jButton.setToolTipText("图片按钮");

        // 按钮加到容器上
        contentPane.add(jButton);
        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);

    }

    public static void main(String[] args) {
        new JButtonDemo01();
    }
} 
```

结果：  
![Demo15](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo15.png)

单选按钮

```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo02 extends JFrame {
    public JButtonDemo02() {
        Container contentPane = this.getContentPane();
        URL resource = JButtonDemo02.class.getResource("man.jpg");
        ImageIcon imageIcon = new ImageIcon(resource);

        // 单选框
        JRadioButton jRadioButton1 = new JRadioButton("jRadioButton1");
        JRadioButton jRadioButton2 = new JRadioButton("jRadioButton2");
        JRadioButton jRadioButton3 = new JRadioButton("jRadioButton3");

        // 单选框一般会分为一组,一个组中只能选择一个
        ButtonGroup buttonGroup = new ButtonGroup();
        buttonGroup.add(jRadioButton1);
        buttonGroup.add(jRadioButton2);
        buttonGroup.add(jRadioButton3);

        contentPane.add(jRadioButton1,BorderLayout.NORTH);
        contentPane.add(jRadioButton2,BorderLayout.SOUTH);
        contentPane.add(jRadioButton3,BorderLayout.CENTER);

        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JButtonDemo02();
    }
}
```  
结果：  
![Demo16](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo16.png)  

多选按钮  
```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;
import java.net.URL;

public class JButtonDemo03 extends JFrame{
    public JButtonDemo03() {
        Container contentPane = this.getContentPane();
        URL resource = JButtonDemo02.class.getResource("man.jpg");
        ImageIcon imageIcon = new ImageIcon(resource);

        // 多选框
        JCheckBox jCheckBox1 = new JCheckBox("jCheckBox1");
        JCheckBox jCheckBox2 = new JCheckBox("jCheckBox2");
        JCheckBox jCheckBox3 = new JCheckBox("jCheckBox3");

        contentPane.add(jCheckBox1,BorderLayout.NORTH);
        contentPane.add(jCheckBox2,BorderLayout.SOUTH);
        contentPane.add(jCheckBox3,BorderLayout.CENTER);

        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JButtonDemo03();
    }
}
```
结果：  
![Demo17](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo17.png) 

### 4.6 列表
  
* 下拉框
```java
package top.cxy96.java_GUI.lesson7;

import javax.swing.*;
import java.awt.*;

public class TestComboboxDemo01 extends JFrame {
    public TestComboboxDemo01() {
        Container contentPane = this.getContentPane();
        JComboBox status = new JComboBox();

        status.addItem(null);
        status.addItem("正在上映");
        status.addItem("已下架");
        status.addItem("正在热映");

        contentPane.add(status);


        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestComboboxDemo01();
    }
}
```  
结果：  
![Demo18](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo18.png) 

* 列表框
```java
package top.cxy96.java_GUI.lesson7;

import javax.swing.*;
import java.awt.*;
import java.util.Vector;

public class TestComboboxDemo02 extends JFrame {
    public TestComboboxDemo02(){
        Container contentPane = this.getContentPane();

        // 生成列表内容
        // String[] contents = {"1","2","3"};
        Vector contents = new Vector();

        // 列表中需要放入内容
        JList jList = new JList(contents);

        contents.add("one");
        contents.add("two");
        contents.add("three");

        contentPane.add(jList);

        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestComboboxDemo02();
    }
}
```
结果：  
![Demo19](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo19.png) 

- 应用场景
  * 选择地区或一些单个选项
  * 列表，展示信息，一般动态扩容

### 4.7 文本框
```java
package top.cxy96.java_GUI.lesson7;

import javax.swing.*;
import java.awt.*;

public class TestTextDemo01 extends JFrame {
    public TestTextDemo01() {
        Container contentPane = this.getContentPane();

        JTextField jTextField1 = new JTextField("hello");
        JTextField jTextField2 = new JTextField("world",20); // 默认字符个数

        contentPane.add(jTextField1,BorderLayout.NORTH);
        contentPane.add(jTextField2,BorderLayout.SOUTH);

        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestTextDemo01();
    }
}
```

结果：  
![Demo20](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo20.png)

密码框
```java
package top.cxy96.java_GUI.lesson7;

import javax.swing.*;
import java.awt.*;

public class TestTextDemo02 extends JFrame {
    public TestTextDemo02() {
        Container contentPane = this.getContentPane();

        JPasswordField jPasswordField = new JPasswordField(); // ***
        jPasswordField.setEchoChar('*');

        contentPane.add(jPasswordField);

        this.setVisible(true);
        this.setBounds(100,200,500,500);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new TestTextDemo02();
    }
}
```

结果：  
![Demo21](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo21.png) 

文本域

```java
package top.cxy96.java_GUI.lesson6;

import javax.swing.*;
import java.awt.*;

public class JScrollDemoDemo extends JFrame {
    public JScrollDemoDemo() {
        Container contentPane = this.getContentPane();

        // 文本域
        JTextArea jTextArea = new JTextArea(20,50);
        jTextArea.setText("学Java认识Java");
        contentPane.add(jTextArea);

        // Scroll面板
        JScrollPane jScrollPane = new JScrollPane(jTextArea);
        contentPane.add(jScrollPane);


        this.setVisible(true);
        this.setBounds(100,100,300,350);
        this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

    public static void main(String[] args) {
        new JScrollDemoDemo();
    }
}
```

结果：  
![Demo22](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_GUI_Demo14.png) 