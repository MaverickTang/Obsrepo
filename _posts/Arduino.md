---
title: Arduino代码整理
date: 2022-07-29 16:42:31
tags:
- 硬件开发
- Arduino
- C
- 代码
categories: 程序笔记
top: False

---

既然要学电子，趁着自己还有C++的编程基础，不如来入门Arduino，做些有意思的项目还能继续学习硬件

<!--more-->

## 基本模版

```c++
void setup() {// 只运行一次，设置引脚还有各种协议
	pinMode(led,OUTPUT);//(引脚编号（int），引脚模式（OUTPUT,INPUT，INPUT_PULLUP（相当于接上电阻保护））)
  Serial.begin(9600);//（整型，串口通信波特率，只有双方用相同的波特率才能通信，波特率越大，通信速率越高）
}

void loop() {//重复运行，像是主函数
	digitalWrite(led,HIGH);//（引脚编号，输出电平（HIGH（5V），LOW（0V）））
  int state=digitalRead(in);//（引脚编号），读取类型为整型
  delay(1000);//（int型，毫秒）
  while(digitalRead(pin)==HIGH){}//等待按键按下
  analogRead(pin);//通过PWM（脉冲宽度调制）实现模拟输出功能，引脚上有“~”标志
}
```

### 串口通信

```c++
void setup() {// 只运行一次，设置引脚还有各种协议
  Serial.begin(9600);//（整型，串口通信波特率，只有双方用相同的波特率才能通信，波特率越大，通信速率越高）
}

void loop() {//重复运行，像是主函数
  while(Serial.available()>0){//如果串口有数据
    char ch=Serial.read();//从SARM中取出1kb的数据
    Serial.println(ch);//串口打出到电脑
  }
  //小插曲：时间函数
  millis();//系统运行时间，单位毫秒，unsigned long类型
  micros();
}
```

##  I/O口高级函数

### 蜂鸣器

```c++
#include "pitches.h"
// notes in the melody:
int melody[] = {
  NOTE_C4, NOTE_G3, NOTE_G3, NOTE_A3, NOTE_G3, 0, NOTE_B3, NOTE_C4
};
// note durations: 4 = quarter note, 8 = eighth note, etc.:
int noteDurations[] = {
  4, 8, 8, 4, 4, 4, 4, 4
};
void setup() {
  // iterate over the notes of the melody:
  for (int thisNote = 0; thisNote < 8; thisNote++) {
    // to calculate the note duration, take one second divided by the note type.
    //e.g. quarter note = 1000 / 4, eighth note = 1000/8, etc.
    int noteDuration = 1000 / noteDurations[thisNote];
    tone(8, melody[thisNote], noteDuration);
    // to distinguish the notes, set a minimum time between them.
    // the note's duration + 30% seems to work well:
    int pauseBetweenNotes = noteDuration * 1.30;
    delay(pauseBetweenNotes);
    // stop the tone playing:
    noTone(8);
  }
}
void loop() {
  // no need to repeat the melody.
}
```

### 脉冲宽度与超声波测距

**PulseIn()**

检测指定引脚的脉冲信号宽度

polseIn(pin, value,timeout);

timeout设置超时

返回值为脉冲宽度，单位为微秒，没有检测到则返回0

**超声波测距**

在发射时计时，测来回时间，测量范围是3～450cm

### ADC参考电压

analogRead(pin)函数返回值=（被测电压/参考电压）*1023

默认参考电压是5V

analogReference(type);

设置Arduino使用外部参考电压

### 外部中断

中断模式：响应中断的处理程序

LOW：低电位触发；CHANGE：电平变化触发；RISING：上升沿触发，低电平变高电平；FALLING：下降沿触发

#### attachInterrupt(interrupt, function,mode)

对中断引脚进行初始化配置

interrupt中断编号（引脚编号），function中断函数名，mode中断模式

#### detachInterrupt(interrupt)

禁用外部中断

# 使用和编写类库

通常一个类包含两个部分，public和private（和java一样）

SR04.h类示范

```c++
# if ARDUINO >=100//判断版本引用系统库，提高兼容性
	#include"Arduino.h"
# else
	#include"Wprogram.h"
# endif

#ifndef SR04_H//标识符后面跟程序段
#define SR04_H
#include "Arduino.h"

class SR04 {
public:
	SR04(int TrigPin,int EchoPin);
	float GetDistance();

private:
	int Trig_pin;
	int Echo_pin;
	float distance;
};
#endif
```

SR04.cpp

```c++
#include "Arduino.h"
#include "SR04.h"
 
SR04::SR04(int TP, int EP){//使用域操作符“::”来说明该函数作用于SR04类
   pinMode(TP,OUTPUT);
   pinMode(EP,INPUT);
   Trig_pin=TP;
   Echo_pin=EP;
}
 
float SR04::GetDistance(){
	digitalWrite(Trig_pin, LOW); 
	delayMicroseconds(2); 
	digitalWrite(Trig_pin, HIGH); 
	delayMicroseconds(10);
	digitalWrite(Trig_pin, LOW); 
	float distance = pulseIn(Echo_pin, HIGH) / 58.00;
	return distance;
}
```


.ino示例程序

```
#include <SR04.h>

SR04 ultrasonic = SR04(2,3);
void setup()
{
  Serial.begin(9600); 
}
void loop()
{
  float distance=ultrasonic.GetDistance();
  Serial.print(distance);
  Serial.print("cm");
  Serial.println(); 
}
```

 # 通信

Arduino与外部数据通信采用串行通信（相对并行通信（需要多个I/O口））

## 串口

UART(Universal Asynchronous Receiver Transmitter),通用异步（串行）收/发口

两个串口设备间需要发射端（TX）与接受端（RX）交叉相连，并共用电源地（GND）

### 串口工作原理

数据传输以数字信号（电平高低变化）的形式进行

**起始位**：总为低电平，是一组数据帧开始传输的信号

**数据位**：承载了实际发送的数据的数据段，Arduino默认8位数据位

**校验位**：检错方式，可以设置为奇校验与偶校验，Arduino默认无校验

**停止位**：每段数据帧最后表示该段数据传输完毕。停止位总为高电平，可以设为一位或两位

### HardwareSerial

**Serial.available()**：获取串口接收到的数据个数

**Serial.begin(speed,config)**：初始化串口，config可以设置数据位，校验位，停止位

**Serial.end()**：结束串口通信

**Serial.find(target)**：从串口缓冲区读取数据，直到找到指定字符串(target)，返回值为boolean

**Serial.findUntil(target,terminal)**:terminal是停止符

**Serial.flush()**:等待数据传输完成（Arduino1.0版以前是清空缓冲区）

**Serial.parseInt()**:从串口流中查找第一个有效的整型数据

**Serial.peek()**:返回1字节的数据，但不会从接受缓冲区删除该数据

**Serial.read()**：从串口读取数据，每读取1字节，就会从缓冲区移除一字节数据

**Serial.readBytes(buffer, length)**：从缓冲区读取指定长度的字符并存入数组(buffer)中

**Serial.readBytesUntil(character,buffer, length)**：从缓冲区读取指定长度的字符并存入数组(buffer)中，如果遇到停止符（character），或者等待数据时间超时，则退出

**Serial.setTimeout(time)**：设置超时时间，单位毫秒

**Serial.print(val,format)**:先转化为字符，再发送ASCII码出去

format分两种情况

进制形式：BIN（二进制）,DEC（十进制）,OCT（8进制）,HEX（16进制）

float位数

**Serial.write(val)**：输出数据到串口，此时发送的是数据本身

### 串口事件

```C++
String inputString = "";         // a String to hold incoming data
bool stringComplete = false;  // whether the string is complete

void setup() {
  // initialize serial:
  Serial.begin(9600);
  // reserve 200 bytes for the inputString:
  inputString.reserve(200);
}

void loop() {
  // print the string when a newline arrives:
  if (stringComplete) {
    Serial.println(inputString);
    // clear the string:
    inputString = "";
    stringComplete = false;
  }
}

/*
  SerialEvent occurs whenever a new data comes in the hardware serial RX. This
  routine is run between each time loop() runs, so using delay inside loop can
  delay response. Multiple bytes of data may be available.
*/
void serialEvent() {
  while (Serial.available()) {
    // get the new byte:
    char inChar = (char)Serial.read();
    // add it to the inputString:
    inputString += inChar;
    // if the incoming character is a newline, set a flag so the main loop can
    // do something about it:
    if (inChar == '\n') {
      stringComplete = true;
    }
  }
}
```

### SoftwareSerial

软件模拟串口通信

通过AVR芯片的PCINT中断功能来实现，因为功能与硬件串口差不多，硬串口的函数也可以用

**SoftwareSerial somename=SoftwareSerial(rxPin,txPin)**：somename软串口对象，rxPin软串口接收脚，txPin软串口发射引脚

**somename.listen()**：开启软串口监听状态，Arduino在同一时间只能监听一个软串口

**somename.isListening()**：检测软串口监听状态，返回Boolean值

**somename.overflow()**：检测软串口缓冲区是否溢出，返回Boolean值

## IIC

[IIC](https://baike.baidu.com/item/iic/3524834)(Inter-Integrated Circuit，IC之间总线)总线，即集成电路总线

用于连接微控制器及其外围设备，是微电子通信控制领域广泛采用的一种总线标准。IIC总线是一个多向控制总线，多个器件（从机）可以同时挂载到一个主机控制的一条总线上，每个连接在总线上的设备都是通过唯一的地址和其他器件通信。与串口的一对一通信方式不同，总线通信通常有主机(Master)和从机(Slave)之分。通信时，主机负责启动和终止数据传送，同时还要输出时钟信号；从机会被主机寻址，并且响应主机的通信请求。

   串口通信双方需要事先约定同样的波特率才能正常进行通信。而在IIC通信中，通信速率的控制由主机完成，主机会通过SCL引脚输出时钟信号供总线上的所有从机使用。 同时，IIC是一种半双工通信方式，即总线上的设备通过SDA引脚传输通信数据，数据的发送和接收由主机控制，切换进行。

        IIC上的所有通信都是由主机发起的，总线上的设备都应该有各自的地址。主机可以通过这些地址向总线上的任一设备发起连接，从机响应请求并建立连接后，便可进行数据传输。IIC总线上的主设备与从设备之间以字节(8位)为单位进行双向的数据传输。
### Wire类库

**begin()**：初始化IIC连接，并作为主机或者从机设备加入IIC总线。当没有填写参数时，设备会以主机模式加人IIC总线；当填写了参数时，设备会以从机模式加入IIC总线，address可以设置为0~127中的任意地址

**Wire.requestFrom(address, quantity, stop)**：主机向从机（address）发送数据请求信号（quantity，请求的字节数）。使用 requestFrom() 后，从机端可以使用 onRequest() 注册一个事件用以响应主机的请求；主机可以通过available() 和 read() 函数读取这些数据。stop，boolean型值，当其值为true时，将发送一个停止信息，释放IIC总线；当为false时，将发送一个重新开始信息，并继续保持IIC总线的有效连接。

**wire.beginTransmission(address)**：设定传输数据到指定地址的从机设备。随后可以使用 write() 函数发送数据，并搭配endTransmission()函数结束数据传输

**Wire.endTransmission(stop)**：结束数据传输。stop, boolean型值，当其值为true时将发送一一个停止信息，释放IIC总线，当没有填写stop参数时，等效使用true；当为false时，将发送一个重新开始信息，并继续保持IIC总线的有效连接。
返回值：byte型值，表示本次传输的状态，取值为：0，成功；1，数据过长，超出发送缓冲区；2，在地址发送时接收到NACK信号,3，在数据发送时接收到NACK信号；4，其他错误。

**write()**：功能：当为主机状态时，主机将要发送的数据加入发送队列；当为从机状态时，从机发送数据至发起请求的主机。
语法:Wire.write(value)，Wire.write(string)，Wire.write(data, length)
参数：value，以单字节发送。string，以一系列字节发送。data，以字节形式发送数组。length，传输的字节数。返回值：byte型值，返回输入的字节数。

**Wire. available()**：返回接收到的字节数。在主机中，一般用于主机发送数据请求后；在从机中，一般用于数据接收事件中。返回值：可读字节数。

**Wire.read()**：读取1B的数据。在主机中，当使用 requestFrom() 函数发送数据请求信号后，需要使用 read() 函数来获取数据；在从机中需要使用该函数读取主机发送来的数据。

**Wire.onReceive(handler)**：该函数可在从机端注册一个事件，当从机收到主机发送的数据时即被触发。handler，当从机接收到数据时可被触发的事件。该事件带有一个int型参数(从主机读到的字节数)且没有返回值，如 void myHandler(int numBytes) 。

**Wire.onRequest(handler)**：注册一个事件,当从机接收到主机的数据请求时即被触发。handler，可被触发的事件。该事件不带参数和返回值，如 voidmyHandler() 。

## SPI

SPI全称Serial Peripheral Interface，即串行外设接口。由Motorola公司提出的一种同步串行数据传输标准。所谓同步，即数据收发双方共用一个时钟；所谓串行，即待传输的数据排成一行，一位一位地传送出去。主要用于微控制器与其他外围设备，如EEPROM、Flash、AD转换器等之间的短距离传输，当然也可实现微控制器与微控制器间的数据传输。相比于其它通信协议，SPI采用四线制的硬件连接方式

![095b7d2e58ed35d4eafa3c581f4518a1.png](https://img-blog.csdnimg.cn/img_convert/095b7d2e58ed35d4eafa3c581f4518a1.png)
