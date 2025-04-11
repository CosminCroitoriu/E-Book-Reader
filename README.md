Nume: Croitoriu Cosmin-Mircea  
Grupă: 332CB

# TSC Project - OpenBook E-Book Reader
Overview
-
This diagram illustrates the hardware architecture of the OpenBook E-Reader, an ESP32-based electronic paper reading device. The system is built around the ESP32-C6-WROOM-1 microcontroller, which interfaces with a 7.5-inch e-Paper display, environmental sensors, and user input buttons.  

![alt text](<Block Diagram-2.jpg>)

***Key Components:*** 

* Core Processing: ESP32-C6 microcontroller with integrated Wi-Fi 6 and BLE 5
* Display: 800×480 resolution e-Paper display connected via SPI
* Sensors: BME688 for temperature, humidity, pressure, and air quality monitoring via I2C
* Power: 2500mAh LiPo battery with fuel gauge and USB-C charging
* Storage: SD card interface for e-book storage via SPI
* Timekeeping: DS3231 RTC with backup power
* User Interface: Buttons via 3xGPIO
* Expansion: QWIIC/Stemma connector for additional peripherals

The firmware is built on FreeRTOS and includes specialized modules for display management, sensor monitoring, battery management, user interface, and e-book rendering. This modular architecture ensures flexible development, easy maintenance, and power-efficient operation—essential for an e-reader device with long battery life requirements.


Power Consumption
-

* In active reading mode (display updated occasionally): ~15-30mA
* In display update mode: ~50-100mA temporarily
* In Wi-Fi active mode: ~120-180mA
* In sleep mode: ~1-5mA
* In deep sleep mode: <50µA

With a 2500mAh battery, the device can operate approximately:

* 100-150 hours in active reading mode (without Wi-Fi)
* 15-20 hours with Wi-Fi constantly active
* Up to 1500 hours (2 months) in deep sleep mode

ESP32-C6 Pin Assignments
-
| Connection Name |   GPIO / Pin Name  | Function  |
|-----------------|------------------|-------------------------------------------------|
| **3V3**         | IO 8             | 3.3V Power line                        |
| **EN (Reset)**  | EN              | Reset Button   |           
| **USB_D-**      | IO12            | USB Data negative, communication  | 
| **USB_D+**      | IO13            | USB Data positive, communication  |
| **Buton Boot**  | IO9             | Bootbutton  |    
| **Buton Change**| IO15            | User input for state changing  |
| **TX (UART)**   | TXD0 / GPIO16   | Serial Transmitter (UART) for communication  |
| **RX (UART)**   | RXD0 / GPIO17   | Serial Receiver (UART) for communication  |
| **SCK (SPI)**   | IO6             | SPI Clock for clock synchronization |
| **MOSI (SPI)**  | IO7             | Transmitter between MC and the Flash, SD Card and display |
| **MISO (SPI)**  | IO2             | Receiver between MC and the Flash, SD Card and display |
| **FLASH_CS**    | IO11            | Flash Chip Select |
| **EPD_CS**      | IO10            | Display Chip select |
| **EPD_DC**      | IO5             | Display Command |
| **EPD_RST**     | IO23            | Display Reset |
| **EPD_BUSY**    | IO3             | Busy Display Signal |
| **SDA (I2C)**   | IO21            | Bidirectional Communication RTC, BME688, Battery Gauge |
| **SCL (I2C)**   | IO22            | I2C synchronization |
| **SS_SD**       | IO4             | SD Card Chip Select |
| **I2C_PW**      | IO19            | Power Control on I2C |
| **EPD_3V3_C**   | IO20            | 3.3V Power Line for the Display |
| **32KHZ**       | IO1             | 32kHz Signal Input |
| **INT_RTC**     | IO0             | RTC DS3231 Interrupt |
| **RTC_RST**     | IO18            | External Reset RTC | 

Bill of Materials
-

| Component | Value | Assigned Part | Where to buy | Datasheet |
| ---------- | --------- | --------- | ---------- | ----- |
| Resistor | 15	$\Omega$ | R_CAPACITOR | [Buy](https://ro.mouser.com/ProductDetail/YAGEO/RT0402FRE0715RL?qs=BXCcY9r%252B08DFFpLSkPOIqQ%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/447/PYu_RT_1_to_0_01_RoHS_L_15-3461507.pdf) |
| Resistor | 200 $\Omega$ | R1_BAT | [Buy](https://ro.mouser.com/ProductDetail/Vishay-Beyschlag/MCS0402MD2000BE100?qs=3SvaY9RawMJNVte4F12%252BZQ%3D%3D) | [Datasheet](https://www.vishay.com/doc?28952) |
| Resistor | 100k $\Omega$ | R_PWRUSB | [Buy](https://ro.mouser.com/ProductDetail/Vishay-Beyschlag/MCT0603PD1003DP500?qs=5aG0NVq1C4wWAn8Ei3OpZA%3D%3D) | [Datasheet](https://www.vishay.com/doc?28916) |
| Resistor | 10k $\Omega$ | R1, R1_PINH1, R1_PINH2, R2-PINH1, R2_PINH2, R4, R5, R6, R7, R8, R9, R10, R_BOOT, R_CHANGE, R_CL1, R_RESET | [Buy](https://ro.mouser.com/ProductDetail/Vishay-Beyschlag/MCS0402MD1002BE000?qs=17u8i%2FzlE8%2F9BrAaXkMk1w%3D%3D) | [Datasheet](https://www.vishay.com/doc?28952) |
| Resistor | 0.47 $\Omega$ | R3 | [Buy](https://ro.mouser.com/ProductDetail/SEI-Stackpole/CSR0402JKR470?qs=IPgv5n7u5QawIB6nBEt8wA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/385/SEI_CSR_CSRN-3077593.pdf) |
| Resistor |  2k $\Omega$ | R2_BAT |[Buy](https://ro.mouser.com/ProductDetail/Vishay-Beyschlag/MCS04020C2001FE000?qs=wTZ%2FFzl837YG0wIkZJJOwQ%3D%3D) | [Datasheet](https://www.vishay.com/doc?28705) |
| Resistor | 2.2 $\Omega$ | R2 | [Buy](https://ro.mouser.com/ProductDetail/SEI-Stackpole/RMCF0402FT2R20?qs=IPgv5n7u5QbBgyl0jwhwsA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/385/SEI_RMCF_RMCP-3077565.pdf) |
| Resistor | 5k1 $\Omega$ | R1_USB, R2_USB | [Buy](https://www.venkel.com/part/TFCR0603-16W-K-5690FT) | [Datasheet](https://data.venkel.com/documents/tfcr-series?_gl=1*tdo8m*_ga*NTA1MTc5MTcyLjE3NDM4OTMzNjc.*_ga_JRKGBZNVM8*MTc0Mzg5MzM2Ni4xLjAuMTc0Mzg5MzM2OC41OC4wLjA.) |
| Capacitor | 10uF | C6 | [Buy](https://ro.mouser.com/ProductDetail/Samsung-Electro-Mechanics/CL10A106KQ8NNNL?qs=xZ%2FP%252Ba9zWqaes9JKSsob2Q%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/585/MLCC-1837944.pdf) |
| Capacitor | 1uF/50V | EPD_C3 | [Buy](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/06035D105MAT2A?qs=k4kUdCzLgS5%252BURKe1SOIeQ%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/40/cx5r_KGM-3223198.pdf) |
| Capacitor | 4.7uF | C1_BAT, C1_BAT1, C2_BAT, C2_BAT1, C4_USB | [Buy](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/0402ZD475MAT2A?qs=NBFAU1oqP4W4U2PCPHI0sg%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/40/cx5r_KGM-3223198.pdf) |
| Capacitor | 100nF | C1, C2, C3_USB, C5, C7, C8, C9, C_DELAY | [Buy](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/06033G104ZAT2A?qs=NXubJDmysXJMPmHfVo6Z%252BA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/40/KGM_Y5V-3223189.pdf) |
| PFMF.050.1 | - | PFMF.050.1 | [Buy](https://ro.mouser.com/ProductDetail/Schurter/PFMF.050.2?qs=1auRipcfynCums5v1iucSA%3D%3D) |  [Datasheet](https://ro.mouser.com/datasheet/2/358/typ_PFMF-1275918.pdf) |
| USB4110-GF-A | - | J2 | [Buy](https://ro.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf) |
| USBLC6-2SC6Y | - | D1 | [Buy](https://ro.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y?qs=gNDSiZmRJS%2FOgDexvXkdow%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/389/usblc6_2sc6y-1852505.pdf) |
| SD0805S020S1R0 | - | D2, D7| [Buy](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/40/schottky-3165252.pdf) |
| DMG2305UX-7 | - | Q1, Q2 | [Buy](https://ro.mouser.com/ProductDetail/Diodes-Incorporated/DMG2305UX-7?qs=L1DZKBg7t5F%2FNBHrjfxC%252Bg%3D%3D) | [Datasheet](https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf) |
| XC6220A331MR-G | - | U5 | [Buy](https://ro.mouser.com/ProductDetail/Torex-Semiconductor/XC6220A331MR-G?qs=AsjdqWjXhJ8ZSWznL1J0gg%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/760/xc6220-3371556.pdf) |
| Capacitor | 100 uF TANT | C_TANT | [Buy](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/TAJW107M010RNJ?qs=Wtp%252Bf%2FAeVqIH8v1VxV%252B1Rg%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/40/TAJ-3165264.pdf) |
| 112A-TAAR-R03_ATTEND | - | J4 | [Buy](https://www.digikey.ro/en/products/detail/attend-technology/112A-TAAR-R03/17633923) | [Datasheet](https://www.attend.com.tw/data/download/file/112A-TAAR-R03_Spec.pdf)
| ESP32-C6-WROOM-1-N8 | - | U1 | [Buy](https://ro.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8?qs=8Wlm6%252BaMh8ST02Gmwp74cw%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/891/Espressif_ESP32_C6_WROOM_1__Datasheet_V0_1_PRELIMI-3239987.pdf) |
| MCP73831 | - | U7 | [Buy](https://ro.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT?qs=yUQqVecv4qvbBQBGbHx0Mw%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/268/MCP73831_Family_Data_Sheet_DS20001984H-3441711.pdf) |
| CHG_LED | - | CHG_LED | [Buy](https://store.comet.srl.ro/Catalogue/Product/40478/) | [Datasheet](https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/datasheet/) |
| SI1308EDL-T1-GE3 | - | Q3 | [Buy](https://ro.mouser.com/ProductDetail/Vishay-Semiconductors/SI1308EDL-T1-GE3?qs=bX1%252BNvsK%2FBramh9tgpOaEw%3D%3D) | [Datasheet](https://www.vishay.com/doc?63399) |
| MBR0530 | - | D3, D4, D5 | [Buy](https://ro.mouser.com/ProductDetail/Micro-Commercial-Components-MCC/MBR0530-T?qs=9VyI4qLX4NTSXkb9ynzJnA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/258/mcc_mbr0520~mbr0560sod123-1179695.pdf) |
| Power Inductor | 68uH | L1 | [Buy](https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D) | [Datasheet](https://www.we-online.com/components/products/datasheet/744043680.pdf) |
| FH34SRJ-24S-0.5SH | - | J1 | [Buy](https://ro.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-24S-0.5SH99?qs=vcbW%252B4%252BSTIpKBl5ap9J8Fw%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/185/FH34SRJ_24S_0_5SH_99__CL0580_1255_6_99_2DDrawing_0-1615044.pdf) |
| BME688 Sensor | - | U8 | [Buy](https://ro.mouser.com/ProductDetail/Bosch-Sensortec/BME688?qs=IS%252B4QmGtzzqQoVDscqwx3A%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/783/bst_bme688_fl000-2307034.pdf) |
| BD5229G-TR | - | U6 |[Buy](https://ro.mouser.com/ProductDetail/ROHM-Semiconductor/BD5229G-TR?qs=4kLU8WoGk0vvnhrrYwdszw%3D%3D) | [Datasheet](https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf) |
| PTS841 Button | - | BOOT_BUTTON, CHANGE_BUTTON, RESET_BUTTON | [Buy](https://ro.mouser.com/ProductDetail/CK/PTS841-ESD-GKP-SMTR-LFS?qs=d0WKAl%252BL4KbeUlwuiSQZWA%3D%3D) | [Datasheet](https://www.ckswitches.com/media/2805/pts841.pdf) |
| MAX17048G+T10 | - | U2 | [Buy](https://ro.mouser.com/ProductDetail/Analog-Devices-Maxim-Integrated/MAX17048G%2bT10?qs=D7PJwyCwLAoGnnn8jEPRBQ%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/609/MAX17048_MAX17049-3469099.pdf) |
| W25Q512JVEIQ | - | U4 | [Buy](https://ro.mouser.com/ProductDetail/Winbond/W25Q512JVEIQ?qs=l7cgNqFNU1jw6svr3at6tA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/949/Winbond_W25Q512JV_Datasheet-3240039.pdf) |
| PGB1010603MR | - | D6, D8, D9, D10, D11, D12 | [Buy](https://ro.mouser.com/ProductDetail/Littelfuse/PGB1010603MRHF?qs=KvZd0dN2Zg%2FuIq6icj%252BGKA%3D%3D) | [Datasheet](https://www.littelfuse.com/media?resourcetype=datasheets&itemid=8a337998-d54d-466b-be4e-dc5bcd1f9321&filename=littelfuse_pulseguard_pgb1_datasheet.pdf) |
| QWIIC_RIGHT_ANGLE | - | J3 | [Buy](https://ro.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf) |
| DS3231SN | - | U3 | [Buy](https://ro.mouser.com/ProductDetail/Analog-Devices-Maxim-Integrated/DS3231SN?qs=ffX8NcjNb2RmKAb9wAk9Ug%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/609/DS3231-3421123.pdf) |
| CPH3225A | - | C_SUPERCAP | [Buy](https://ro.mouser.com/ProductDetail/Seiko-Semiconductors/CPH3225A?qs=3etwrb1wR%252BhUOph6lAO7eg%3D%3D) | [Datasheet](https://ro.mouser.com/datasheet/2/360/Seiko_Instruments_MicroBattery_E_20230330_2024Jan_-3561061.pdf) |

Design Considerations
-

* The modular design allows for individual component updates and easy problem diagnosis
* Using a single LDO regulator to generate 3.3V for the entire board simplifies the power design
* Battery charging is done through the USB-C port, ensuring wide compatibility
* The environmental sensors allow for monitoring the conditions in which the device is used and can be used to alert the user about unfavorable conditions
* Used a predefined 3D model for the screen. Source: https://grabcad.com/library/7-5in-e-ink-display-assortment-1


PCB Observations
-

* PCB Dieletctric layer has been reduced from 1.6mm to 1mm to fit in the case.
* Via Stitching has been applied around the MC, so the impedance of the ground plane is lowered.

Errors and Warnings
- 
* The Board Outline Clearence errors were all approved, as every component was matching the placement in the given document.
* Unconnected Lines warnings are a bug from Fusion, as everytime I try to remove them, the error reappears. 
* Copper Width errors for the inductor were approved as the model matched the one in the givne scheme.



