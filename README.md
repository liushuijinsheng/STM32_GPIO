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
