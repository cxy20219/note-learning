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