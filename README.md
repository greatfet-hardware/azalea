# Azalea

This repository contains the KiCad design for Azalea, also known as GreatFET One.  The design requires:

https://github.com/greatscottgadgets/gsg-kicad-lib

If you are using git, the preferred way to install gsg-kicad-lib is to use the submodule:

```
git submodule init && git submodule update
```

## Overview

Also known as GreatFET One, Azalea is the main board of the GreatFET project.

Azalea is a peripheral interface tool.  By adding expansion boards called "neighbors", you can turn Azalea into a USB peripheral that does almost anything.

Features:
* LPC4330 microcontroller (U1)
* Hi-Speed USB port (USB0) for connection to a host computer
* Expansion interface (J1 and J2) of 80 pins (2 female headers with 2 rows of 20 pins)
* Bonus row of 20 male pins (J7)
* 4 indicator LEDs
* 2 buttons, primarily for development (DFU and RESET, just like HackRF One)
* Full Speed USB port (USB1) for connection to a target (for [Facedancer](https://github.com/usb-tools/Facedancer))
* Power switching for use of USB1 as either host or device
* 3.3 V regulator that can supply some power to neighbors
* 2 MB flash memory
* Unpopulated Cortex Debug Header (J5) for JTAG or SWD

Except where noted below, all pins on expansion ports use 3.3 V I/O voltage.

## J1 (NEIGHBOR1) Pinout

Pin|Symbol|Special Function|Notes    |U1 Pin|GPIO |U0 |U1 |U2  |EMC        |SGPIO|ENET      |CAN1|SSP0|SSP1|I2S0           |I2S1  |USB0     |USB1     |SD   |MISC   |PWM  |TIMER  |SCT     
---|------|----------------|---------|------|-----|---|---|----|-----------|-----|----------|----|----|----|---------------|------|---------|---------|-----|-------|-----|-------|--------
1  |GND   |                |         |      |     |   |   |    |           |     |          |    |    |    |               |      |         |         |     |       |     |       |        
2  |VCC   |                |3.3 V    |      |     |   |   |    |           |     |          |    |    |    |               |      |         |         |     |       |     |       |        
3  |P4_9  |                |         |33    |5[13]|   |   |    |           |14   |          |RD  |    |    |               |      |         |         |     |       |     |       |CTIN_6  
4  |P0_0  |                |         |32    |0[0] |   |   |    |           |0    |RXD1      |    |    |MISO|TX_WS          |TX_WS |         |         |     |       |     |       |        
5  |P4_10 |                |         |35    |5[14]|   |   |    |           |15   |          |    |    |    |               |      |         |         |     |       |     |       |CTIN_2  
6  |P0_1  |                |         |34    |0[1] |   |   |    |           |1    |TX_EN     |    |    |MOSI|               |TX_SDA|         |         |     |       |     |       |        
7  |P1_0  |                |         |38    |0[4] |   |   |    |A5         |7    |          |    |SSEL|    |               |      |         |         |     |       |     |       |CTIN_3  
8  |P5_0  |                |         |37    |2[9] |   |DSR|    |D12        |     |          |    |    |    |               |      |         |         |     |       |MCOB2|T1_CAP0|        
9  |P5_1  |                |         |39    |2[10]|   |DTR|    |D13        |     |          |    |    |    |               |      |         |         |     |       |MCI2 |T1_CAP1|        
10 |P1_1  |boot mode       |pull-up  |42    |0[8] |   |   |    |A6         |8    |          |    |MISO|    |               |      |         |         |     |       |     |       |CTOUT_7 
11 |CLK0  |                |         |45    |     |   |   |    |CLK0, CLK01|     |REF_CLK   |    |    |SCK |               |      |         |         |CLK  |CLKOUT |     |       |        
12 |P1_2  |boot mode       |pull-down|43    |0[9] |   |   |    |A7         |9    |          |    |MOSI|    |               |      |         |         |     |       |     |       |CTOUT_6 
13 |P1_5  |                |         |48    |1[8] |   |   |    |CS0#       |15   |          |    |    |SSEL|               |      |PWR_FAULT|         |POW  |       |     |       |CTOUT_10
14 |P5_2  |                |         |46    |2[11]|   |RTS|    |D14        |     |          |    |    |    |               |      |         |         |     |       |MCI1 |T1_CAP2|        
15 |P1_7  |                |         |50    |1[0] |   |DSR|    |D0         |     |          |    |    |    |               |      |PPWR     |         |     |       |     |       |CTIN_1  
16 |P1_6  |                |         |49    |1[9] |   |   |    |WE#        |14   |          |    |    |    |               |      |         |         |CMD  |       |     |       |CTIN_5  
17 |P1_9  |                |         |52    |1[2] |   |RTS|    |D2         |     |          |    |    |    |               |      |         |         |DAT0 |       |     |       |CTOUT_11
18 |P1_8  |                |         |51    |1[1] |   |DTR|    |D1         |     |          |    |    |    |               |      |         |         |VOLT0|       |     |       |CTOUT_12
19 |P5_3  |                |         |54    |2[12]|   |RI |    |D15        |     |          |    |    |    |               |      |         |         |     |       |MCI0 |T1_CAP3|        
20 |P1_10 |                |         |53    |1[3] |   |RI |    |D3         |     |          |    |    |    |               |      |         |         |DAT1 |       |     |       |CTOUT_14
21 |P1_12 |                |         |56    |1[5] |   |DCD|    |D5         |8    |          |    |    |    |               |      |         |         |DAT3 |       |     |T0_CAP1|        
22 |P1_11 |                |         |55    |1[4] |   |CTS|    |D4         |     |          |    |    |    |               |      |         |         |DAT2 |       |     |       |CTOUT_15
23 |P5_5  |                |         |58    |2[14]|   |DCD|    |D9         |     |          |    |    |    |               |      |         |         |     |       |MCOA1|T1_MAT1|        
24 |P5_4  |                |         |57    |2[13]|   |CTS|    |D8         |     |          |    |    |    |               |      |         |         |     |       |MCOB0|T1_MAT0|        
25 |P1_14 |                |         |61    |1[7] |   |RXD|    |D7         |10   |          |    |    |    |               |      |         |         |     |       |     |T0_MAT2|        
26 |P1_13 |                |         |60    |1[6] |   |TXD|    |D6         |9    |          |    |    |    |               |      |         |         |CD   |       |     |T0_CAP0|        
27 |P5_6  |                |         |63    |2[15]|   |TXD|    |D10        |     |          |    |    |    |               |      |         |         |     |       |MCOB1|T1_MAT2|        
28 |P1_15 |                |         |62    |0[2] |   |   |TXD |           |2    |RXD0      |    |    |    |               |      |         |         |     |       |     |T0_MAT1|        
29 |P5_7  |                |         |65    |2[7] |   |RXD|    |D11        |     |          |    |    |    |               |      |         |         |     |       |     |T1_MAT3|        
30 |P1_16 |                |         |64    |0[3] |   |   |RXD |           |3    |CRS, RX_DV|    |    |    |               |      |         |         |     |       |MCOA2|T0_MAT0|        
31 |P1_18 |                |         |67    |0[13]|   |   |DIR |           |12   |TXD0      |RD  |    |    |               |      |         |         |     |       |     |T0_MAT3|        
32 |P1_17 |                |         |66    |0[12]|   |   |UCLK|           |11   |MDIO      |TD  |    |    |               |      |         |         |     |       |     |T0_CAP3|        
33 |P9_5  |                |         |69    |5[18]|TXD|   |    |           |3    |          |    |    |    |               |      |         |PPWR     |     |       |MCOA1|       |        
34 |P9_6  |                |         |72    |4[11]|RXD|   |    |           |8    |          |    |    |    |               |      |         |PWR_FAULT|     |       |MCOB1|       |        
35 |P2_0  |                |         |75    |5[0] |TXD|   |    |A13        |4    |MDC       |    |    |    |               |      |PPWR     |         |     |ISP_TXD|     |T3_CAP0|        
36 |P6_0  |                |         |73    |     |   |   |    |           |     |          |    |    |    |RX_MCLK, RX_SCK|      |         |         |     |       |     |       |        
37 |P1_20 |                |         |70    |0[15]|   |   |    |           |13   |TXD1      |    |    |SSEL|               |      |         |         |     |       |     |T0_CAP2|        
38 |P1_19 |                |         |68    |     |   |   |    |           |     |REF_CLK   |    |    |SCK |RX_MCLK        |TX_SCK|         |         |     |CLKOUT |     |       |        
39 |P1_4  |                |         |47    |0[11]|   |   |    |BLS0#      |11   |          |    |    |MOSI|               |      |IND0     |         |VOLT1|       |     |       |CTOUT_9 
40 |P1_3  |                |         |44    |0[10]|   |   |    |OE#        |10   |          |    |    |MISO|               |      |IND1     |         |     |       |     |       |CTOUT_8 

## J2 (NEIGHBOR2) Pinout

Pin|Symbol  |Special Function|Notes            |U1 Pin|GPIO |U0  |U1 |U2 |U3  |EMC        |SGPIO|RMII|CAN0|CAN1|SPI |SSP0      |SSP1|SPIFI|I2S0                            |I2S1  |I2C0|I2C1|USB0     |USB1|SD |ADC     |MISC              |PWM  |TIMER  |SCT     
---|--------|----------------|-----------------|------|-----|----|---|---|----|-----------|-----|----|----|----|----|----------|----|-----|--------------------------------|------|----|----|---------|----|---|--------|------------------|-----|-------|--------
1  |GND     |                |                 |      |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |        
2  |5V      |                |                 |      |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |        
3  |P4_8    |                |                 |15    |5[12]|    |   |   |    |           |13   |    |    |TD  |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTIN_5  
4  |P4_0    |                |                 |1     |2[0] |    |   |   |UCLK|           |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |NMI               |MCOA0|       |        
5  |ADC0_0  |                |                 |6     |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |0_0, 1_0|DAC               |     |       |        
6  |P4_5    |                |                 |10    |2[5] |    |   |   |    |           |11   |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTOUT_5 
7  |P4_4    |                |                 |9     |2[4] |    |   |   |DIR |           |10   |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |DAC               |     |       |CTOUT_2 
8  |P4_2    |                |                 |8     |2[2] |    |   |   |RXD |           |8    |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTOUT_0 
9  |P4_3    |                |                 |7     |2[3] |    |   |   |BAUD|           |9    |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |0_0     |                  |     |       |CTOUT_3 
10 |P4_6    |                |                 |11    |2[6] |    |   |   |    |           |12   |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTOUT_4 
11 |P4_7    |                |                 |14    |     |    |   |   |    |           |     |    |    |    |    |          |    |     |TX_SCK                          |TX_SCK|    |    |         |    |   |        |GP_CLKIN          |     |       |        
12 |CLK2    |                |                 |99    |     |    |   |   |    |CLK3, CLK23|     |    |    |    |    |          |    |     |TX_MCLK                         |RX_SCK|    |    |         |    |CLK|        |CLKOUT            |     |       |        
13 |P2_8    |DFU, boot mode  |pull-down, button|98    |5[7] |    |   |   |DIR |A8         |15   |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTOUT_0 
14 |P2_7    |ISP, boot mode  |pull-up          |96    |0[7] |    |   |   |UCLK|A9         |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |T3_MAT3|CTOUT_1 
15 |P2_6    |                |                 |95    |5[6] |DIR |   |   |    |A10        |7    |    |    |    |    |          |    |     |                                |      |    |    |IND0     |    |   |        |                  |     |T3_CAP3|CTIN_7  
16 |P7_7    |                |                 |140   |3[15]|    |   |   |    |           |7    |MDC |    |    |    |          |    |     |                                |      |    |    |         |    |   |1_6     |TRACEDATA[3]      |     |       |CTOUT_8 
17 |WAKEUP0 |                |pull-up          |130   |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |WAKEUP0           |     |       |        
18 |P2_5    |                |                 |91    |5[5] |    |   |   |    |           |14   |    |    |    |    |          |    |     |                                |      |    |    |IND0     |VBUS|   |TRIG1   |                  |     |T3_MAT2|CTIN_2  
19 |P2_4    |                |                 |88    |5[4] |    |   |   |RXD |           |13   |    |    |    |    |          |    |     |                                |      |    |SCL |PWR_FAULT|    |   |        |                  |     |T3_MAT1|CTIN_0  
20 |P2_3    |                |                 |87    |5[3] |    |   |   |TXD |           |12   |    |    |    |    |          |    |     |                                |      |    |SDA |PPWR     |    |   |        |                  |     |T3_MAT0|CTIN_1  
21 |PF_4    |                |                 |120   |     |    |   |   |    |           |     |    |    |    |    |          |SCK |     |TX_MCLK, RX_SCK                 |      |    |    |         |    |   |        |GP_CLKIN, TRACECLK|     |       |        
22 |P3_2    |                |                 |116   |5[9] |    |   |   |    |           |     |    |TD  |    |    |          |    |     |TX_SDA, RX_SDA                  |      |    |    |         |IND0|   |        |                  |     |       |        
23 |P7_2    |                |                 |115   |3[10]|    |   |RXD|    |           |6    |    |    |    |    |          |    |     |TX_SDA                          |      |    |    |         |    |   |        |                  |     |       |CTIN_4  
24 |P3_1    |                |                 |114   |5[8] |    |   |   |    |           |     |    |RD  |    |    |          |    |     |TX_WS, RX_WS                    |      |    |    |         |IND1|   |        |                  |     |       |        
25 |P7_1    |                |                 |113   |3[9] |    |   |TXD|    |           |5    |    |    |    |    |          |    |     |TX_WS                           |      |    |    |         |    |   |        |                  |     |       |CTOUT_15
26 |P3_0    |                |                 |112   |     |    |   |   |    |           |     |    |    |    |    |SCK       |    |     |RX_SCK, RX_MCLK, TX_SCK, TX_MCLK|      |    |    |         |    |   |        |                  |     |       |        
27 |P7_0    |                |                 |110   |3[8] |    |   |   |    |           |4    |    |    |    |    |          |    |     |                                |      |    |    |         |    |   |        |                  |     |       |CTOUT_14
28 |P3_4    |                |                 |119   |1[14]|    |TXD|   |    |           |     |    |    |    |    |          |    |SIO3 |TX_WS                           |RX_SDA|    |    |         |    |   |        |                  |     |       |        
29 |P6_8    |                |                 |86    |5[16]|    |   |   |    |A14        |7    |    |    |    |    |          |    |     |                                |      |    |    |IND0     |    |   |        |                  |     |T2_MAT1|        
30 |P3_7    |                |                 |123   |5[10]|    |   |   |    |           |     |    |    |    |MOSI|MISO, MOSI|    |MOSI |                                |      |    |    |         |    |   |        |                  |     |       |        
31 |P6_7    |                |                 |85    |5[15]|    |   |   |    |A15        |6    |    |    |    |    |          |    |     |                                |      |    |    |IND1     |    |   |        |                  |     |T2_MAT0|        
32 |P3_3    |                |                 |118   |     |    |   |   |    |           |     |    |    |    |SCK |SCK       |    |SCK  |TX_MCLK                         |TX_SCK|    |    |         |    |   |        |CGU_OUT1          |     |       |        
33 |P2_2    |                |                 |84    |5[2] |UCLK|   |   |    |A11        |6    |    |    |    |    |          |    |     |                                |      |    |    |IND1     |    |   |        |                  |     |T3_CAP2|CTIN_6  
34 |P6_6    |                |                 |83    |0[5] |    |   |   |    |BLS1#      |5    |    |    |    |    |          |    |     |                                |      |    |    |PWR_FAULT|    |   |        |                  |     |T2_CAP3|        
35 |P2_1    | neighbor WC    |                 |81    |5[1] |RXD |   |   |    |A12        |5    |    |    |    |    |          |    |     |                                |      |    |    |PWR_FAULT|    |   |        |ISP_RXD           |     |T3_CAP1|        
36 |P6_3    |                |                 |79    |3[2] |    |   |   |    |CS1#       |4    |    |    |    |    |          |    |     |                                |      |    |    |PPWR     |    |   |        |                  |     |T2_CAP2|        
37 |P3_5    |                |                 |121   |1[15]|    |RXD|   |    |           |     |    |    |    |    |          |    |SIO2 |TX_SDA                          |RX_WS |    |    |         |    |   |        |                  |     |       |        
38 |P3_6    |                |                 |122   |0[6] |    |   |   |    |           |     |    |    |    |MISO|SSEL, MISO|    |MISO |                                |      |    |    |         |    |   |        |                  |     |       |        
39 |I2C0_SDA|                |pull-up          |93    |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |SDA |    |         |    |   |        |                  |     |       |        
40 |I2C0_SCL|                |pull-up          |92    |     |    |   |   |    |           |     |    |    |    |    |          |    |     |                                |      |SCL |    |         |    |   |        |                  |     |       |        

## J5 (JTAG) Pinout

Pin|Symbol    |Notes          |U1 Pin
---|----------|---------------|------
1  |VCC       |3.3 V          |      
2  |TMS/SWDIO |               |30    
3  |GND       |               |      
4  |TCK/SWDCLK|pull-up        |27    
5  |GND       |               |      
6  |TDO/SWO   |pull-up        |31    
7  |          |not connected  |      
8  |TDI       |               |26    
9  |GND       |               |      
10 |RESET#    |pull-up, button|128   

## J7 (BONUS_ROW) Pinout

Pin|Symbol       |Special Function|Notes          |U1 Pin|GPIO |U0  |U2  |U3  |EMC    |I2S0  |ADC     |PWM    |TIMER  |SCT    
---|-------------|----------------|---------------|------|-----|----|----|----|-------|------|--------|-------|-------|-------
1  |GND          |                |               |      |     |    |    |    |       |      |        |       |       |       
2  |P6_4         |                |               |80    |3[3] |TXD |    |    |CAS#   |      |        |       |       |CTIN_6 
3  |P6_5         |                |               |82    |3[4] |RXD |    |    |RAS#   |      |        |       |       |CTOUT_6
4  |ADC0_5/ADC1_5|                |               |144   |     |    |    |    |       |      |0_5, 1_5|       |       |       
5  |ADC0_2/ADC1_2|                |               |143   |     |    |    |    |       |      |0_2, 1_2|       |       |       
6  |P2_9         |boot mode       |pull-down      |102   |1[10]|    |    |BAUD|A0     |      |        |       |       |CTOUT_3
7  |P2_12        |                |               |106   |1[12]|    |UCLK|    |A3     |      |        |       |       |CTOUT_4
8  |P2_13        |                |               |108   |1[13]|    |DIR |    |A4     |      |        |       |       |CTIN_4 
9  |RTC_ALARM    |                |               |129   |     |    |    |    |       |      |        |       |       |       
10 |RTCX1        |                |               |      |     |    |    |    |       |      |        |       |       |       
11 |RESET#       |                |pull-up, button|128   |     |    |    |    |       |      |        |       |       |       
12 |VBAT         |                |               |127   |     |    |    |    |       |      |        |       |       |       
13 |P2_11        |                |               |105   |1[11]|    |RXD |    |A2     |      |        |       |       |CTOUT_5
14 |P2_10        |                |               |104   |0[14]|    |TXD |    |A1     |      |        |       |       |CTOUT_2
15 |P6_10        |                |               |100   |3[6] |    |    |    |DQMOUT1|      |        |MCABORT|       |       
16 |P6_9         |                |               |97    |3[5] |    |    |    |DYCS0# |      |        |       |T2_MAT2|       
17 |P6_2         |                |               |78    |3[1] |DIR |    |    |CKEOUT1|RX_SDA|        |       |T2_CAP1|       
18 |P6_1         |                |               |74    |3[0] |UCLK|    |    |DYCS1# |RX_WS |        |       |T2_CAP0|       
19 |GND          |                |               |      |     |    |    |    |       |      |        |       |       |       
20 |VCC          |                |3.3 V          |      |     |    |    |    |       |      |        |       |       |       
