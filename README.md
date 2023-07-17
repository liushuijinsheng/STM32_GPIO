# STM32_GPIO学习  
GPIO输出四种模式：1、推挽输出  低电平输出0
                          高电平输出3V3
              2、开漏输出  低电平接地  
                           无法直接输出高电平，为高阻态（电路分析时作断路）
注：开漏输出一般应用在 I2C、 SMBUS 通讯等需要“线与”功能的总线电路中。除此之外，还用在电
平不匹配的场合，如需要输出 5 伏的高电平，就可以在外部接一个上拉电阻，上拉电源为 5 伏，
并且把 GPIO 设置为开漏模式，当输出高阻态时，由上拉电阻和电源向外输出 5 伏的电平
              浮空输出(Floating):输出处于高阻态
              模拟输入(Analog):GPIO用于模拟输入


每个GPI/O端口有两个32位配置寄存器(GPIOx_CRL， GPIOx_CRH)，两个32位数据寄存器
(GPIOx_IDR和GPIOx_ODR)，一个32位置位/复位寄存器(GPIOx_BSRR)，一个16位复位寄存
器(GPIOx_BRR)和一个32位锁定寄存器(GPIOx_LCKR)


GPIO输入四种模式

浮空输入(Floating Input)
这是GPIO默认的输入模式,此时如果不配置,GPIO口既不上拉也不下拉,状态为高阻态,易受到Noise干扰。

下拉输入(Pull-Down Input)
GPIO内部通过下拉电阻接到地,默认状态为低电平。常用于按钮、开关等。

上拉输入(Pull-Up Input)
GPIO内部通过上拉电阻接到电源,默认状态为高电平。常用于I2C总线。

模拟输入(Analog Input)
GPIO输入连接到ADC,用于模拟量输入采集。


上面是GPIO端口的设置，下面是标准库GPIO的使用

新建一个.h文件存放头文件，即包含函数声明和宏定义；一个.c文件存放程序文件。

.h中

#ifndef __文件名_H
#define	__文件名_H

//更换自己的库文件
#include "stm32f10x.h"

//宏定义串口时钟以及搭载的APB2还是APB1
#define LED_G_PORT    		GPIOC			             
#define LED_G_CLK 	   	  RCC_APB2Periph_GPIOC		
#define LED_G_PIN		    	GPIO_Pin_0			        

//定义函数
void LED_GPIO_Config(void);	
void LED_G_ON (void);	
void LED_G_OFF (void);

.c中
#include "文件名.h"

void BEEP_GPIO_Config(void)
{		
    //定义一个GPIO_InitStructure的结构体
		GPIO_InitTypeDef GPIO_InitStructure;
    //使能RCC的时钟
		RCC_APB2PeriphClockCmd(LED_G_CLK , ENABLE); 
		//设置GPIO串口												   
		GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0;	
    //设置GPIO输出模式为推挽输出	
		GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;   
    //设置GPIO速率为50Mhz
		GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz; 
    //调用库函数，初始化LED的GPIO
		GPIO_Init(LED_G_PORT, &GPIO_InitStructure);			 
}



具体举2个例子
1、点亮LED


2、按键检测（案件已经硬件消抖）
