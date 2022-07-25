## OLED 坐标轴

oled驱动需要 安装SSD1306

```c
// x,y 
void Oled_init(){
  display.clearDisplay();
  display.drawFastHLine(8,56,120,SSD1306_WHITE);
  display.drawFastVLine(8,0,56,SSD1306_WHITE);
  // 设置字体颜色,白色可见
  display.setTextColor(WHITE);
  //设置字体大小
  display.setTextSize(1);
  display.setCursor(0, 1);
  display.print("d");

  display.setCursor(120, 57);
  display.print("t");
}
```

## 超声波测距

```c
float get_destance(){
  digitalWrite(5,LOW);
  delayMicroseconds(2);
  digitalWrite(5,HIGH);
  delayMicroseconds(10);
  digitalWrite(5,LOW);
  float distance = pulseIn(4,HIGH)/58.00;
  return distance;
}
```

## DHT 温湿度

安装DHT库与 Adafruit Unified Sensor

```c
#include "DHT.h"
#define DHTPIN 2     // 数字接受引脚
#define DHTTYPE DHT11  // 类型 1s
//#define DHTTYPE DHT22   // 2s

DHT dht(DHTPIN, DHTTYPE);
// 初始化传感器
dht.begin();
void show_t_h(){
   delay(1000);

  // 湿度
  float h = dht.readHumidity();
  // 华氏摄氏度
  float t = dht.readTemperature();
  // 摄氏度
  float f = dht.readTemperature(true);
  // 华氏摄氏度热指数
  float hif = dht.computeHeatIndex(f, h);
  // 摄氏度热指数
  float hic = dht.computeHeatIndex(t, h, false);
}
```

