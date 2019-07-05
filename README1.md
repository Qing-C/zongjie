# 开源硬件实战课程
> 老师 **damo 王**
> 2019/07/02-07/05

> 汇报人 曹茸 18030100226
# 第一天
## 入门介绍
* 为什么要学习开源硬件
* 如何学习开源硬件 
多**练习**、多看**原版网站**
* 创建GitHub账号
* 安装arduino、fritzing、processing

![arduino](https://graph.baidu.com/resource/1119d4f866236b4b684fb01562303638.jpg) ![fritzing](https://graph.baidu.com/resource/111f564541f8c1fd31bf501562303561.jpg) ![processing](https://graph.baidu.com/resource/111524f104763a1363b9401562303548.jpg)

# 第二天
## arduino编程
* Morse代码

```#include <Morse.h>

Morse mor(13);
char incomingByte;
String strMorse;

void setup() 
{
  Serial.begin(9600);
}

void loop() 
{
  if(Serial.available() > 0)
  incomingByte = Serial.read();
  Serial.print(incomingByte);
  if (isLowerCase(incomingByte))
  {
    switch(incomingByte){
      case 'a' : strMorse = String("*-"); break;
      case 'b' : strMorse = String("-***"); break;
      case 'c' : strMorse = String("-*-*"); break;
      case 'd' : strMorse = String("-**"); break;
      case 'e' : strMorse = String("*"); break;
      case 'f' : strMorse = String("**-*"); break;
      case 'g' : strMorse = String("--*"); break;
      case 'h' : strMorse = String("****"); break;
      case 'i' : strMorse = String("**"); break;
      case 'j' : strMorse = String("*---"); break;
      case 'k' : strMorse = String("-*-"); break;
      case 'l' : strMorse = String("*-**"); break;
      case 'm' : strMorse = String("--"); break;
      case 'n' : strMorse = String("-*"); break;
      case 'o' : strMorse = String("---"); break;
      case 'p' : strMorse = String("*--*"); break;
      case 'q' : strMorse = String("--*-"); break;
      case 'r' : strMorse = String("*-*"); break;
      case 's' : strMorse = String("***"); break;
      case 't' : strMorse = String("-"); break;
      case 'u' : strMorse = String("**-"); break;
      case 'v' : strMorse = String("***-"); break;
      case 'w' : strMorse = String("*--"); break;
      case 'x' : strMorse = String("-**-"); break;
      case 'y' : strMorse = String("-*--"); break;
      case 'z' : strMorse = String("--**"); break;
      }
      int i = 0;
      while(strMorse[i])
      {
        if (strMorse[i] == '*')
        {
          mor.dot();
        }
        if (strMorse[i] == '-')
        {
          mor.dash();
        }
        i++;
      }
      mor.c_space();
    }
    if(isWhitespace(incomingByte))
    {
      mor.w_space();
    }
    if(incomingByte == '\n')
    {
      delay(3000);
    }
}
```
* 库函数形式
```
Morse.h
Morse.cpp
```
# 第三天
## 认识电子元器件及操作
* 小车代码和电路图
![car](https://graph.baidu.com/resource/111cb558aa698d99e446501562304151.jpg)
```
void setup()
{
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  Serial.begin(9600);
}
int income = 0;
void loop()
{
  if(Serial.available() > 0)
  {
    income = Serial.read();
      switch(income)
      {
        case 'f':forward(); break;
        case 'b':backward(); break;
        case 'l':left(); break;
        case 'r':right(); break;
        case 's':stop(); break;
      }
  }
}
void forward()
{
  digitalWrite(5,HIGH);
  digitalWrite(6,LOW);
  digitalWrite(9,HIGH);
  digitalWrite(10,LOW);
}

void backward()
{
  digitalWrite(6,HIGH);
  digitalWrite(5,LOW);
  digitalWrite(10,HIGH);
  digitalWrite(9,LOW);
}

void left()
{
  digitalWrite(5,HIGH);
  digitalWrite(6,LOW);
  digitalWrite(10,HIGH);
  digitalWrite(9,LOW);
}

void right()
{
  digitalWrite(6,HIGH);
  digitalWrite(5,LOW);
  digitalWrite(9,HIGH);
  digitalWrite(10,LOW);
}

void stop()
{
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);
  digitalWrite(10,LOW);
}
```
* 数码管代码和电路图
![数码管](https://graph.baidu.com/resource/11107dcee7f6a9998017701562304281.jpg)
```
void setup()
{
  pinMode(0, OUTPUT);
  pinMode(1, OUTPUT);
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  Serial.begin(9600);
}

int income = 0;
void loop()
{
  digitalWrite(0,LOW);
  digitalWrite(1,LOW);
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
  digitalWrite(4,LOW);
  
  if(Serial.available() > 0)
  {
    income = Serial.read();
    Serial.println(income,DEC);
    switch(income)
    {
      case '0':show0();break;
      case '1':show1();break;
      case '2':show2();break;
      case '3':show3();break;
      case '4':show4();break;
      case '5':show5();break;
      case '6':show6();break;
      case '7':show7();break;
      case '8':show8();break;
      case '9':show9();break;
    }
  }
  delay(10);
}
void show0()
{
  digitalWrite(0,LOW);
  digitalWrite(1,LOW);
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
}
void show1()
{
  digitalWrite(0,HIGH);
  digitalWrite(1,LOW);
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
}
void show2()
{
  digitalWrite(0,LOW);
  digitalWrite(1,HIGH);
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
}
void show3()
{
  digitalWrite(0,HIGH);
  digitalWrite(1,HIGH);
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
}
void show4()
{
  digitalWrite(0,LOW);
  digitalWrite(1,LOW);
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
}
void show5()
{
  digitalWrite(0,HIGH);
  digitalWrite(1,LOW);
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
}
void show6()
{
  digitalWrite(0,LOW);
  digitalWrite(1,HIGH);
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
}
void show7()
{
  digitalWrite(0,HIGH);
  digitalWrite(1,HIGH);
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
}
void show8()
{
  digitalWrite(0,LOW);
  digitalWrite(1,LOW);
  digitalWrite(2,LOW);
  digitalWrite(3,HIGH);
}
void show9()
{
  digitalWrite(0,HIGH);
  digitalWrite(1,LOW);
  digitalWrite(2,LOW);
  digitalWrite(3,HIGH);
}
```
# 第四天
## 总结
* Morse代码thinkcad可运行代码
（因为07/03的Morse代码接过板子，可运行，此处不再多写）
* markdown格式学习总结