## 1. Hello World实验
```arduino
int val;
int ledPin=13;
void setup() {
  Serial.begin(9600); //设置波特率为9600
  pinMode(ledPin,OUTPUT); //设置13口 为输出模式
}
void loop() {
  val=Serial.read(); //读取pc发送的指令
  if(val=='R'){      //指令为R则点亮led
      digitalWrite(ledPin,HIGH);
      delay(500);
      digitalWrite(ledPin,LOW);
      delay(500);
      Serial.println("Hello World"); //打印字符串
    }
}
```

## 2. Led闪烁实验
```arduino
int ledPin=10;
void setup() {
  pinMode(ledPin,OUTPUT); //初始化10口为输出模式
}

void loop() {
  digitalWrite(ledPin,HIGH); //输出高电压
  delay(1000);               //延时一秒
  digitalWrite(ledPin,LOW);  //输出低电压
  delay(500);                //延时500秒 
}
```

## 3. 按键控制Led
```arduino
int ledPin=11;
int inPin=7;
int val;
void setup() {
  pinMode(ledPin,OUTPUT);
  pinMode(inPin,INPUT); //定义7口为输入模式
}

void loop() {
  val=digitalRead(inPin); //读取数字7口的电平值
  if(val==LOW){
      digitalWrite(ledPin,LOW);
    }
  else{
      digitalWrite(ledPin,HIGH);
    }6

}
```

## 4. 交通灯设计实验
```arduino
int redLed=10;
int yellowLed=7;
int greenLed=4;
void setup() {
  pinMode(redLed,OUTPUT);
  pinMode(yellowLed,OUTPUT);
  pinMode(greenLed,OUTPUT);
}
void loop() {
  digitalWrite(redLed,HIGH);
  delay(1000);
  digitalWrite(redLed,LOW);
  digitalWrite(yellowLed,HIGH);
  delay(200);
  digitalWrite(yellowLed,LOW);
  digitalWrite(greenLed,HIGH);
  delay(1000);
  digitalWrite(greenLed,LOW);

}
```
## 5. 广告灯效果实验
```arduino
int BASE = 2; // 第一个Led I/O脚
int NUM = 6; // LED的数量
void setup() {
  for(int i=BASE;i<BASE+NUM;i++){
      pinMode(i,OUTPUT);    
  }
}

void loop() {
  for(int i=BASE;i<BASE+NUM;i++){
      digitalWrite(i,LOW);
      delay(200); // 延时200毫秒   
  }
  for(int i=BASE;i<BASE+NUM;i++){
      digitalWrite(i,HIGH);
      delay(200); // 延时200毫秒   
  }
}
```
## 6. PWM灯光调控亮度实验
```aduino
int potIn = 0;   //定义模拟接口0
int ledPin = 3;  //定义数字接口11(PWM输出)
int val;        //暂存来自传感器的变量
void setup() {
  pinMode(ledPin,OUTPUT); //定义数字接口为输出
  Serial.begin(9600);

  //模拟接口自动设置为输入
}

void loop() {
  val=analogRead(potIn);      //读取传感器模拟值
  val=map(val,0,1023,0,255); //将val映射到0~255
  Serial.println(val);       //输出模拟值
  analogWrite(ledPin,val);    //PWM最高输出255
  delay(10);                  //延时0.01秒
}
```
## 7. 抢答器设计实验
```arduino
int greenPin=5;
int yellowPin=6;
int redPin=7;
int greenLed=10;
int yellowLed=9;
int redLed=8;
int red;
int yellow;
int green;
void setup() {
  pinMode(greenLed,OUTPUT);
  pinMode(yellowLed,OUTPUT);
  pinMode(redLed,OUTPUT);
  pinMode(greenPin,INPUT);
  pinMode(yellowPin,INPUT);
  pinMode(redPin,INPUT);
}

void loop() {
  red=digitalRead(redPin);
  if(red==LOW){
      digitalWrite(redLed,LOW);
    }
  else{
      digitalWrite(redLed,HIGH);
    }
  green=digitalRead(greenPin);
  if(green==LOW){
      digitalWrite(greenLed,LOW);
    }
  else{
      digitalWrite(greenLed,HIGH);
    }
  yellow=digitalRead(yellowPin);
  if(yellow==LOW){
      digitalWrite(yellowLed,LOW);
    }
  else{
      digitalWrite(yellowLed,HIGH);
    }
}
```
## 8. 倾斜开关实验
```arduino
void setup() {
  pinMode(8,OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int i;
  i=analogRead(5);
  if(i>250){
    digitalWrite(8,HIGH);
  }
  else{
    digitalWrite(8,LOW);
  }
  delay(10);
}

```

## 9. 有源蜂鸣器实验
```arduino
int buzzer=9;
void setup() {
  pinMode(buzzer,OUTPUT);
}

void loop() {
  digitalWrite(buzzer,HIGH);
  delay(100);
  digitalWrite(buzzer,LOW);
  delay(100);
}
```
## 10. 无源蜂鸣器实验
```arduino
int buzzer=9;
void setup() {
  pinMode(buzzer,OUTPUT);
}
void loop()
{
for(int i=200;i<=800;i++)                    //用循环的方式将频率从200HZ 增加到800HZ
{
  pinMode(buzzer,OUTPUT);
  tone(buzzer,i);                            //在四号端口输出频率
delay(5);                              //该频率维持5毫秒   
}
delay(4000);                            //最高频率下维持4秒钟
for(int i=800;i>=200;i--)
{
  pinMode(buzzer,OUTPUT);
  tone(buzzer,i);
delay(10);
}
}
```
## 11. 模拟值读取实验
```arduino
int potPin=0;
int ledPin=9;
int val;
void setup() {
  pinMode(ledPin,OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(ledPin,HIGH);
  val=analogRead(potPin);
  Serial.println(val);
}
```
## 12. 光控声音实验
```arduino
int buzzer=9;
void setup() {
  pinMode(buzzer,OUTPUT);
}

void loop() {
  digitalWrite(buzzer,HIGH);
  delay(100);
  digitalWrite(buzzer,LOW);
  delay(100);
}
```
## 13. RGB LED实验
```arduino
int redPin = 11;
int greenPin = 10;
int bluePin = 9;
 
void setup()
{
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);  
}
 
void loop()
{
  setColor(255, 0, 0);  // 红色
  delay(1000);
  setColor(0, 255, 0);  // 绿色
  delay(1000);
  setColor(0, 0, 255);  // 蓝色
  delay(1000);
  setColor(255, 255, 0);  // 黄色
  delay(1000);  
  setColor(80, 0, 80);  // 紫色
  delay(1000);
  setColor(0, 255, 255);  // 浅绿色
  delay(1000);
}
 
void setColor(int red, int green, int blue)
{
  analogWrite(redPin, 255-red);
  analogWrite(greenPin, 255-green);
  analogWrite(bluePin, 255-blue);  
}
```
## 14
## 15