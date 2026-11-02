# Wardriver!

<img src="images/side shot.png" width="1000">

#

### wardriving (noun) - The act of searching for a Wi-Fi wireless network, usually from a moving vehicle, using a laptop or smartphone.
#

<p align="center">
  <img src="images/front.png" width="45%">
  <img src="images/back.png" width="45%">
</p>


Hello yall! (My second README, have fun! <3) so this is a... wardriver! Well I like to call it a wi-fi/BLE scanner and monitor and I won't scan while from a moving vehicle but wardriver sounds cooler so yeah.
#
This is my second project which I actually did it all by myself (not unlike the software projects, let's not talk about those.)


This device scans wi-fi and bluetooth RFs and it also has GPS, and it uses the ESP32 Marauder (by justcallmekoko).

#
### This is the PCB 
<p align="center">
  <img src="images/pcb1.png" width="45%">
  <img src="images/pcb2.png" width="45%">
</p>
you can find it in the repo files aswell (duh), along with the schematic, and all those files.

### This is the Schematic
<img src="images/Schematic.png" width="500">

#

#### I have also made an edit, which is on the *'doomscroller'* of Half-Life, as soon as I have a link (from anywhere) I will post it here. 

What else can I say, this project is a very interesting project and I am passionate on such things, on Radio Frequencies, scanning them, etc. and I have been wanting to make it for a long time. Its like when I think about it my heart starts racing with excitement! 


## NEW, THE ONE AND ONLY **ENCLOSUREEE**
Alright, I have made the enclosure too, took a bit, but its worth it, it looks LOVELYYY.
#
Images!
#
<img src="images/case/case_front.png" width="1000">

#

<p align="center">
  <img src="images/case/case1.png" width="30%">
  <img src="images/case/Third.png" width="60.6%">
</p>
<p align="center">
  <img src="images/case/case_boom.png" width="35.85%">
  <img src="images/case/second_Picture.png" width="55%">
</p>


## Firmware

THE FIRMWARE. Yah the reviewer told me that I need it in here so here it is.

**ESP32 Marauder** by justcallmekoko
Source: https://github.com/justcallmekoko/ESP32Marauder
Pinned release: **v1.20.0**, 28 Oct 2026, https://github.com/justcallmekoko/ESP32Marauder/releases/tag/v1.20.0


### Pin mapping

| Module pad | GPIO | Net | Connects to |
|---|---|---|---|
| 3 | EN | RESET | SW2, reset button |
| 4 | GPIO4 | VBAT_SENSE | 100k/100k divider off BAT, ADC1_CH3 |
| 5 | GPIO5 | BTN_SEL | SW5, select |
| 6 | GPIO6 | BTN_BACK | SW6, back |
| 10 | GPIO17 | GPS_TX | NEO-M8N TX, so ESP receive |
| 11 | GPIO18 | GPS_RX | NEO-M8N RX, so ESP transmit |
| 12 | GPIO8 | SD_CS | microSD chip select on the display module |
| 13 | GPIO19 | USB_DN | USB-C D- |
| 14 | GPIO20 | USB_DP | USB-C D+ |
| 17 | GPIO9 | TFT_RST | ILI9341 reset |
| 18 | GPIO10 | TFT_CS | ILI9341 chip select |
| 19 | GPIO11 | MOSI | shared SPI, display and SD |
| 20 | GPIO12 | SCLK | shared SPI, display and SD |
| 21 | GPIO13 | MISO | shared SPI, display and SD |
| 22 | GPIO14 | TFT_DC | ILI9341 data/command |
| 23 | GPIO21 | TFT_LED | display backlight |
| 27 | GPIO0 | BOOT | SW1, boot button |
| 31 | GPIO38 | LED1 | status LED through 330R |
| 32 | GPIO39 | LED2 | status LED through 330R |
| 33 | GPIO40 | LED3 | status LED through 330R |
| 38 | GPIO2 | BTN_DOWN | SW4, down |
| 39 | GPIO1 | BTN_UP | SW3, up |



### Board config

```c
#define ILI9341_DRIVER
#define TFT_WIDTH  240
#define TFT_HEIGHT 320

#define TFT_MISO 13
#define TFT_MOSI 11
#define TFT_SCLK 12
#define TFT_CS   10
#define TFT_DC   14
#define TFT_RST   9
#define TFT_BL   21
#define TFT_BACKLIGHT_ON HIGH

#define SPI_FREQUENCY 40000000
```

Then a target block in `esp32_marauder/configs.h`.

```c
#ifdef MARAUDER_WARDRIVER
  #define HAS_BT
  #define HAS_BUTTONS
  #define HAS_SCREEN
  #define HAS_GPS
  #define HAS_SD
  #define USE_SD
  #define HAS_BATTERY
  #define HAS_PSRAM
#endif

// buttons, all active low to GND with internal pullups
#ifdef MARAUDER_WARDRIVER
  #define U_BTN  1
  #define D_BTN  2
  #define C_BTN  5
  #define B_BTN  6
  #define L_BTN -1
  #define R_BTN -1
  #define HAS_U
  #define HAS_D
  #define HAS_C
  #define U_PULL true
  #define D_PULL true
  #define C_PULL true
  #define L_PULL true
  #define R_PULL true
#endif

// microSD shares the display SPI bus
#ifdef MARAUDER_WARDRIVER
  #define SD_CS 8
  #define SD_MISO TFT_MISO
  #define SD_MOSI TFT_MOSI
  #define SD_SCK  TFT_SCLK
#endif

// NEO-M8N on UART1, 9600 baud default
#ifdef MARAUDER_WARDRIVER
  #define GPS_SERIAL_INDEX 1
  #define GPS_RX 17
  #define GPS_TX 18
#endif
```


## And yes, of course, the BOM;
(BOM v1, I will cut costs to land under 65$, OR I will work more and make it fully finished for tier 3 of funding who knows :3)

|Part|Qty|Price|Link|
|---|---|---|---|
| ESP32-S3-WROOM-1U-N16R8 | 1 | $6.76/32.24 RON | https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1U-N16R8/16162641 |
| 2.2" SPI TFT, ILI9341, 240×320, with microSD | 1 | $13.88/66.11 RON | https://www.amazon.com/Display-Module-240x320-ILI9341-Arduino/dp/B0F9XXV4V7?currency=USD |
| GY-NEO-M8N GPS module + patch antenna | 1 | $17.45 | https://www.addicore.com/products/neo-m8n-gps-gnss-module-with-eeprom |
| TP4056 Lithium Battery Charger Module with Dual Protection (USB-C) | 1 | $4.95/23.58 RON | https://www.crcibernetica.com/tp4056-lithium-battery-charger-module-with-dual-protection-usb-c/ | 
| AP2112K-3.3 | 1 | $0.17/0.81 RON | https://www.lcsc.com/product-detail/C51118.html |
| A03401A | 1 | $0.52/2.48 RON| https://www.digikey.com/en/products/detail/alpha-omega-semiconductor-inc/AO3401A/1855773
| SS34 Schottky | 1 | $1.01/4.81 | https://www.digikey.com/en/products/detail/onsemi/SS34/1052384 |
| TYPE-C-31-M-12 | 1 | $0.19/0.90 RON | https://jlcpcb.com/partdetail/Korean_HropartsElec-TYPE_C_31_M12/ |
| Keystone 1042 18650 holder | 1 | $5.99/28.53 RON | https://www.digikey.com/en/products/detail/keystone-electronics/1042/2745668 | 
| Samsung INR18650-35E 3400mAh cell, flat top | 1 | $7.37/35.12 RON | https://botland.store/li-ion-batteries/15216-18650-li-ion-samsung-inr18650-35e-3400mah-5904422343071.html |
| B3S-1000 | 6(10 pack) | $4.24/20.20 RON| https://www.digikey.com/en/products/detail/aratas-formerly-omron-components/b3s-1000/20686
| slide switch, SPDT | 1 | $0.75/3.57RON | https://www.digikey.com/en/products/detail/c-k/OS102011MA1QN1/1981430 |
| LED 0805 | 3 | $0.38/1.81 RON | https://www.digikey.com/en/products/detail/visual-communications-company-vcc/LSM0805452V/10229619 | 
| 220 ohm resistor | 3 | $0.30/1.43 RON | https://www.digikey.com/en/products/detail/yageo/RC0805JR-07330RL/728311 |
| 10k ohm resistor | 3 | $0.33/1.57 RON | https://www.digikey.com/en/products/detail/vishay-dale/CRCW080510K0FKEAC/7928398 |
| 100k ohm resistor | 3 | $0.30/1.43 RON | https://www.digikey.com/en/products/detail/yageo/RC0805JR-07100KL/728239 |
| 5.1k ohm resistor | 2 | $0.2/0.95 RON | https://www.digikey.com/en/products/detail/yageo/RC0805JR-075K1L/728338 |
| 100nF capacitor | 4 | $0.72/3.43 RON | https://www.digikey.com/en/products/detail/kemet/C0805C104K5RACTU/411169
| 1uF capacitor | 1 | $0.67/3.19 RON | https://eu.mouser.com/en/ProductDetail/KYOCERA-AVX/KAF21KR71H105JU?qs=sGAEpiMZZMsh%252B1woXyUXjwCqkQtzlfA8HMiLPMH3N9o%3D |
| 10uF capacitor | 3 | $1.02/4.86 RON | https://www.digikey.com/en/products/detail/yageo/CC0805ZKY5V6BB106/2103093 |
| 22uF capacitor | 2 | $0.72/3.43 RON | https://www.digikey.com/en/products/detail/murata-electronics/GRM21BR61E226ME44L/4905535 |
| PCB from JLCPCB | 5 pack | $4.00/19.05 RON | N/A |
