---
layout: post
title: Arduino LCD 1602 Keypad Shield实例代码（带DFROBOT字样的那种）
date: 2015-03-19 07:15:28
categories: 技术
tags: Arduino
---

买东西的地方给的kuaipan的地址，但是貌似关闭分享功能了。去淘宝找了一下卖类似东东的网店，终于发现一家直接把代码贴上来了。我试验了一下，可用。纯属没地方放，另外给搜索过来的朋友做个参考，整段代码贴上来当做笔记。1602应该是四线模式，几个按键应该是模拟方式，也就是不支持多键同时按下。RST键会直接RESET。

```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(8, 13, 9, 4, 5, 6, 7);

char msgs[5][16] = {
    "Right Key OK ",  
    "Up Key OK ",  
    "Down Key OK ",  
    "Left Key OK ",  
    "Select Key OK" 
};

int adc_key_val[5] ={50, 200, 400, 600, 800 };  
int NUM_KEYS = 5;  
int adc_key_in;  
int key=-1;  
int oldkey=-1;

void setup() {  
    // put your setup code here, to run once:  
    lcd.clear();  
    lcd.begin(16, 2);  
    lcd.setCursor(0,0);  
    lcd.print("ADC key testing");  
}

void loop() {  
    // put your main code here, to run repeatedly:  
    adc_key_in = analogRead(0); // read the value from the sensor  
    key = get_key(adc_key_in); // convert into key press  
  
    if (key != oldkey) // if keypress is detected  
    {  
        delay(50); // wait for debounce time  
        adc_key_in = analogRead(0); // read the value from the sensor  
        key = get_key(adc_key_in); // convert into key press  
        if (key != oldkey)  
        {  
            lcd.setCursor(0, 1);  
            oldkey = key;  
            if (key >=0){  
                lcd.print(msgs[key]);  
            }  
        }  
    }  
    delay(100);  
}

// Convert ADC value to key number  
int get_key(unsigned int input)  
{  
    int k;  
  
    for (k = 0; k < NUM_KEYS; k++)  
    {  
        if (input < adc_key_val[k])  
        {  
            return k;  
        }  
    }  
  
    if (k >= NUM_KEYS)k = -1; // No valid key pressed  
    return k;  
}

```
