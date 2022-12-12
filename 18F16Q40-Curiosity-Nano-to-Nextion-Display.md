# Curosity Nano to Nextion display
![Nextion](https://github.com/chrissavage2300/chrissavage2300.github.io/blob/main/photos/Nextion_Display.jpg?raw=true)

This page deals with the code on both the microcontroller side and HMI (nextion) side of things to get these two talking without a library. 
I had to figure some of this out on my own, so I want to share some of the knowledge I found along the way. In the end, you can say I started to make a library, but this is much more readable than the usual stuff you can find.

Parts used:

 <ul>
  <li>PIC18F16Q40 CURIOSITY NANO </li>
  <li>Nextion NX3224T024</li>
  <li>USB to UART converter (anyone works)</li> 
</ul> 

Software:

 <ul>
  <li>Nextion Editor V1.63.3</li>
  <li>MPLAB X V6.00</li>
  <li>XC8 V2.20 or better</li>
  <li>MPLAB Code Configurator V5</li> 
  
</ul> 

This project assumes you know how to use the above software. The very first thing we want to do is to define a UART port. For this, I used RB5 and RB7. I only used them because they were right next to each other. You can use whatever you want. Set your USART to 9600 BPS.

The onboard LED is tied to RC1, so be sure to set this as an output. You can use another pin if you want, just dont forget to define it. 

Setting up the Nano was pretty simple after that. The default settings work well.

(SETTINGS PLACE HOLDER)

Be sure that when you select UART1 that you check the box that says "Redirect STDIO to UART"


First we want to declare some variables we will be using for this. 
```c
 unsigned char FAN;//FAN button
 __bit LED_Status_BIT;//Just a LED status bit
 char buf[16];//character buffer
```
Next, we want to make a function. This is basically a UART buffer than receives x amount of characters from the UART lines.
```c
void EUSART_Read_Text(char *Output, unsigned int length)
{
 unsigned int j;
 for(j=0;j<length;j++)
 Output[j] = UART1_Read();
}
```
Put this at the top of your c file, before void main that gets generated. Now we are ready to read characters from the Nextion display.

This is what it should look like:
```c
#include "mcc_generated_files/mcc.h"
#include <stdio.h>
#include <string.h>
/*
                         Main application
 */

unsigned char FAN;
char buf[16];
 
//This function reads characters coming in from the USART port from the nextion
void EUSART_Read_Text(char *Output, unsigned int length)
{
	unsigned int j;
	for(j=0;j<length;j++)
	Output[j] = UART1_Read();
}
       
void main(void)
{
    // Initialize the device
    SYSTEM_Initialize();

    while (1)
    { 
     
    
    }
}

```


[back](./)
