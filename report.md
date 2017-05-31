# 游戏交互技术个人作业
### 2014011347  张轩

## 作业1
代码如下所示

```
/*------------音符对应蜂鸣器频率------------*/

#define B0  31
#define C1  33
#define CS1 35
#define D1  37
#define DS1 39
#define E1  41
#define F1  44
#define FS1 46
#define G1  49
#define GS1 52
#define A1  55
#define AS1 58
#define B1  62
#define C2  65
#define CS2 69
#define D2  73
#define DS2 78
#define E2  82
#define F2  87
#define FS2 93
#define G2  98
#define GS2 104
#define A2  110
#define AS2 117
#define B2  123
#define C3  131
#define CS3 139
#define D3  147
#define DS3 156
#define E3  165
#define F3  175
#define FS3 185
#define G3  196
#define GS3 208
#define A3  220
#define AS3 233
#define B3  247
#define C4  262
#define CS4 277
#define D4  294
#define DS4 311
#define E4  330
#define F4  349
#define FS4 370
#define G4  392
#define GS4 415
#define A4  440
#define AS4 466
#define B4  494
#define C5  523
#define CS5 554
#define D5  587
#define DS5 622
#define E5  659
#define F5  698
#define FS5 740
#define G5  784
#define GS5 831
#define A5  880
#define AS5 932
#define B5  988
#define C6  1047
#define CS6 1109
#define D6  1175
#define DS6 1245
#define E6  1319
#define F6  1397
#define FS6 1480
#define G6  1568
#define GS6 1661
#define A6  1760
#define AS6 1865
#define B6  1976
#define C7  2093
#define CS7 2217
#define D7  2349
#define DS7 2489
#define E7  2637
#define F7  2794
#define FS7 2960
#define G7  3136
#define GS7 3322
#define A7  3520
#define AS7 3729
#define B7  3951
#define C8  4186
#define CS8 4435
#define D8  4699
#define DS8 4978

#define buzzer_pin 8 //定义蜂鸣器引脚

/*------------定义歌曲音调的数组------------*/

int notes[] = {
  C6, B5, A5, G5, E5, F5, G5, G5, A5, B5, C6, G5, G5, C6, B5, C6
};

/*------------定义歌曲节奏的数组------------*/

byte beats[] = {
  600, 250, 250, 500, 250, 125, 375, 250, 250, 250, 1250, 150, 150, 250, 125, 625
};

void setup() {
  pinMode(buzzer_pin, OUTPUT); //定义蜂鸣器引脚为输出状态
}

void loop() {
  for ( int i = 0; i < 16; i++) {

/*------------设置i在歌曲长度内递增，这样就能逐一执行数组中的数据------------*/

    tone(buzzer_pin, notes[i]); //播放音乐
    delay(beats[i] * 1.5); //播放间隔

    noTone(buzzer_pin);
    delay(50);
    if (i==10) delay(250);
  }
  delay(30000);
}
```
### 运行注意：

- 该部件只需要一个蜂鸣器部件，应接到D8
- 烧录程序后即可听到循环播放的铃声


## 作业2

代码如下所示

```
#include <Adafruit_NeoPixel.h>  //调用LED彩灯的库文件

Adafruit_NeoPixel ColorLED = Adafruit_NeoPixel(1, 6, NEO_GRB + NEO_KHZ800);

void setup() {
  ColorLED.begin();
  pinMode(A0, INPUT); //设置光敏传感器引脚为输入状态
  pinMode(A2, INPUT);
  Serial.begin(9600); //设置串口波特率为9600
}

void loop() {
  int state1 = analogRead(A0);
  int state2 = analogRead(A2);
  if (state1 > 50) state1 = 0;
  else state1 = 1;
  if (state2 > 100) state2 = 1;
  else state2 = 0;
  if (state1 & state2) {
    while(true) {
      ColorLED.setPixelColor(0, ColorLED.Color(255, 0, 0));  //设置彩灯颜色为红色
      ColorLED.show();  //显示彩灯效果
      delay(5000);
      state2 = analogRead(A2);
      if (state2 <= 100) break;
    }
    ColorLED.setPixelColor(0, ColorLED.Color(0, 0, 0));  //设置彩灯颜色为红色
    ColorLED.show();  //显示彩灯效果
  }
}
```

## 运行注意：
- 需要连接三个部件：彩灯、光敏传感器、声音传感器
- 光敏传感器连接至A0，声音传感器连接至A2
- 彩灯连接至D6
- 用手捂住光敏传感器（或在暗处测试），然后对着声音传感器对话即可亮灯，五秒后若检测不到声音则会灭灯


## 作业3

代码如下所示

```
/*------------音符对应蜂鸣器频率------------*/
#include <Microduino_Key.h> //调用开关的库文件

#define B0  31
#define C1  33
#define CS1 35
#define D1  37
#define DS1 39
#define E1  41
#define F1  44
#define FS1 46
#define G1  49
#define GS1 52
#define A1  55
#define AS1 58
#define B1  62
#define C2  65
#define CS2 69
#define D2  73
#define DS2 78
#define E2  82
#define F2  87
#define FS2 93
#define G2  98
#define GS2 104
#define A2  110
#define AS2 117
#define B2  123
#define C3  131
#define CS3 139
#define D3  147
#define DS3 156
#define E3  165
#define F3  175
#define FS3 185
#define G3  196
#define GS3 208
#define A3  220
#define AS3 233
#define B3  247
#define C4  262
#define CS4 277
#define D4  294
#define DS4 311
#define E4  330
#define F4  349
#define FS4 370
#define G4  392
#define GS4 415
#define A4  440
#define AS4 466
#define B4  494
#define C5  523
#define CS5 554
#define D5  587
#define DS5 622
#define E5  659
#define F5  698
#define FS5 740
#define G5  784
#define GS5 831
#define A5  880
#define AS5 932
#define B5  988
#define C6  1047
#define CS6 1109
#define D6  1175
#define DS6 1245
#define E6  1319
#define F6  1397
#define FS6 1480
#define G6  1568
#define GS6 1661
#define A6  1760
#define AS6 1865
#define B6  1976
#define C7  2093
#define CS7 2217
#define D7  2349
#define DS7 2489
#define E7  2637
#define F7  2794
#define FS7 2960
#define G7  3136
#define GS7 3322
#define A7  3520
#define AS7 3729
#define B7  3951
#define C8  4186
#define CS8 4435
#define D8  4699
#define DS8 4978

#define buzzer_pin 8 //定义蜂鸣器引脚

/*------------定义歌曲音调的数组------------*/
Key KeyA(2, INPUT_PULLUP); //定义开关参数

volatile int state = 0;
#define SONG 0x2
#define PLAY 0x1

int notes[] = {
  C6, B5, A5, G5, E5, F5, G5, G5, A5, B5, C6, G5, G5, C6, B5, C6
};

int notes2[] = {E5, E5, F5, G5, G5, F5, E5, D5, C5, C5, D5, E5, E5, D5, D5};

/*------------定义歌曲节奏的数组------------*/

byte beats[] = {
  600, 250, 250, 500, 250, 125, 375, 250, 250, 250, 1250, 150, 150, 250, 125, 625
};

byte beats2[] = {250, 250, 250, 250, 250, 250, 250, 250, 250, 250, 250, 250, 375, 125, 500};

void setup() {
  pinMode(buzzer_pin, OUTPUT); //定义蜂鸣器引脚为输出状态
  pinMode(2, INPUT); //设置开关引脚为输入状态
  Serial.begin(9600); //设置串口波特率为9600
  attachInterrupt(0, blink, FALLING);
}

void loop() {
 // delay(300000);
  if (state & PLAY) {
    if (state & SONG) {
      for (int i = 0; i < 15; i++) {
        tone(buzzer_pin, notes2[i]); //播放音乐
        delay(beats2[i] * 1.5); //播放间隔
        noTone(buzzer_pin);
        delay(50);
        if (!(state & PLAY)) break;
        if (!(state & SONG)) break;
      }
    }
    else {
      for (int i = 0; i < 16; i++) {
        tone(buzzer_pin, notes[i]); //播放音乐
        delay(beats[i] * 1.5); //播放间隔
        noTone(buzzer_pin);
        delay(50);
        if (i==10) delay(250);
        if (!(state & PLAY)) break;
        if (state & SONG) break;
      }
    }
  }
}

volatile unsigned long last = 0;
volatile unsigned long current = 0;

void blink() {
  current = millis();
  if (current - last < 200) {
    return;
  }
  Serial.println(last);
  Serial.println(current);
  noTone(buzzer_pin);
  if (current - last < 1000) {
    volatile byte i = bitRead(state, 1);
    bitWrite(state, 1, (1 - i));
    bitSet(state, 0);
  }
  else {
    volatile byte i = bitRead(state, 0);
    bitWrite(state, 0, (1 - i));
  }
  Serial.println(state);
  Serial.println();
  last = current;
}
```
### 创意简介：
- 该代码是对作业1的一个改进，通过增加一个碰撞传感器（即抖动开关），实现对音乐播放的控制
- 以iphone的耳机控制器为参考，给出两个主要控制功能的实现
- 1.单按按钮，让音乐播放/暂停
- 2.连按两次按钮，播放下一首音乐
- demo中只存放了两首音乐。另外，由于硬件本身具有一定的问题（开关防抖性较差使得第二个功能的检测比较难），实测下会有一定的不稳定因素（代码做了简单的处理，但我还没有对硬件本身的防抖参数做进一步的测试）。
- 由于delay特性，这里采用了中断的处理方式，可以保证及时响应开关处理请求

### 运行注意：
- 除将蜂鸣器接至D8口，还需要将开关接至D2口
- 连接完毕后，烧录程序，可以用开关控制音乐的进行
