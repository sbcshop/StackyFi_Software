# StackyFi_Software

<img src= "https://cdn.shopify.com/s/files/1/1217/2104/files/Main_Banner_3.png?v=1729493200" />

This GitHub provides getting started instructions to use StackyFi board.

### Features
- Powered by ESP32 S3 which is having Dual-core Arm Cortex-M0+ processor, flexible running up to 133 MHz
- Its WiFi/BLE capabilities make it suited for a variety of IoT applications
- Standard 40-pin GPIO header to accommodate most Raspberry Pi-compatible HATs.
- CSI camera connectors provide versatile connectivity for camera modules, making them suited for a variety of imaging applications
- The 6D IMU sensor (Inertial Measurement Unit) provides comprehensive motion tracking with six degrees of freedom, combining accelerometer and gyroscope data for precise orientation and movement sensing
- WS2812B RGB LED for adding varied activity status
- Power and charging LEDs for status indication
- Battery connection and charging facilities for portability
- Onboard microSD card compatibility is useful for data logging projects
- Both Serial and Native USB are available as Type C
- Boot and Reset Buttons for programming purposes

<!--
## Specification:
- **Microcontroller**  : ESP32-S3 series of SoCs having Xtensa® dual-core 32-bit LX7 microprocessor
- **Connectivity** : 2.4 GHz Wi-Fi (802.11 b/g/n) and Bluetooth® 5 (LE)
- **Memory** : Flash up to 16 MB, PSRAM up to 8 MB
- **Board Supply Voltage** : 5V 
- **Operating Pin Voltage** : 3.3V 
- **GPIOs connector** : JST-SH-1MM-8 pin
- **RTC module**: DS3231 
- **Coin Cell Holder** : Supports CR1220 3V Battery
- **Battery Connector** : Supports 3.7V Lithium ion battery  
- **Battery Charge Management** : MCP73831
- **RGB LED** : WS2812B
- **Working Temperature** : 0°C ~ +40°C 
- **E-Paper Display** =>
  - **E-paper Size** : 7.5"
  - **Resolution** : 800x480
  - **Color** : Red, Black and White
  - **Interface** : SPI
  - **Driver** : UC8179


## Getting Started with EnkFi 7.5" Board
### Pinout
<img src= "https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/images/EnkFi_7.5_pinout.png" />

| | | |
|--|--|--|
|(1) Power LED          | (7) Buzzer                      | (13) Boot Button |
|(2) Charging Status    | (8) GPIOs Breakout              | (14) Reset Button |
|(3) Battery Connector  | (9) TF card slot                | (15) Programmable Buttons |
|(4) E-paper connector  | (10) Native USB (USB_D+/USB_D-) | (16) Programmable Buttons  |
|(5) DS3231 RTC         | (11) Serial USB                 | (17) 7.5” E-Paper Display |
|(6) Coin Cell Holder   | (12) ESP32 S3 WROOM-1           | |
  
### Interfacing Details
  
- **_E-Paper Display interfacing with ESP32_**

  | ESP32 | Display | Function |
  |---|---|---|
  | IO12 | DISPLAY_SCK_PIN  | Clock pin of SPI interface for E-Paper Display |
  | IO11 | DISPLAY_MOSI_PIN | MOSI (Master OUT Slave IN) pin of SPI interface|
  | IO13 | DISPLAY_DC_PIN   | Data/Command (MISO) pin of SPI interface |
  | IO10 | DISPLAY_CS_PIN   | Chip Select pin of SPI interface|
  | IO21 | DISPLAY_BUSY_PIN | Busy Status pin of E-Paper |
  | IO14 | DISPLAY_RST_PIN  | Display Reset pin |

 - **_SDcard Interface_**

   | ESP32 | SDCard | Function |
   |---|---|---|
   | IO42 | CARD_CLK | Clock pin of SPI interface for Display|
   | IO2  | CARD_MOSI | MOSI (Master OUT Slave IN) pin of SPI interface|
   | IO41 | CARD_MISO  | MISO (Master IN Slave OUT) pin of SPI interface|
   | IO1  | CARD_CS  | Chip Select pin of SPI interface|

- **_Buzzer and Buttons Interfacing_**

  | ESP32 | Hardware | Function |
  |---|---|---|
  |IO15 | Buzzer |Buzzer Positive Pin |  
  |IO0 | BOOT |Boot button |
  |IO4 | BT1 | Programmable Button |
  |IO5 | BT2 | Programmable Button |
  |IO6 | BT3 | Programmable Button |
  |IO7 | BT4 | Programmable Button |

- **_DS3231 RTC interfacing with ESP32 using I2C_** 

  | ESP32 | DS3231 | Description | 
  |---|---|---|
  | IO38 | SDA | I2C Serial Data Pin |
  | IO39 | SCL | I2C Serial Clock Pin |

- **_GPIOs Breakout_**

  | ESP32 | Type* | Multi-Function (_**Bold-Italic**_ default Function) |
  |---|---|---|    
  |3V3  | P     | Positive Supply, 3.3V |
  |5V   | P     | Positive Supply, 5V |
  |GND  | P     | Supply Ground |
  |TX   | I/O/T | RTC_GPIO17,**_GPIO17_**,U1TXD,ADC2_CH6 |
  |RX   | I/O/T | RTC_GPIO18,**_GPIO18_**,U1RXD,ADC2_CH7,CLK_OUT3 |
  |IO8  | I/O/T | RTC_GPIO8, _**GPIO8**_ , TOUCH8, ADC1_CH7, SUBSPICS1  |  
  |IO9  | I/O/T | RTC_GPIO9,**_GPIO9_**,TOUCH9,ADC1_CH8,FSPIHD,SUBSPIHD |
  |IO16 | I/O/T | RTC_GPIO16,**_GPIO16_**,U0CTS,ADC2_CH5,XTAL_32K_N |
  |IO40 | I/O/T | MTDO,**_GPIO40_**,CLK_OUT2 |

  *I-INPUT, O-OUTPUT, P-POWER & T-HIGH IMPEDENCE
  
### 1. Configure and Setup Development Environment
   - Download Arduino IDE from [official site](https://www.arduino.cc/en/software) and install into your system. We have use Arduino IDE 1.8.19
   - Once installation done will add ESP32 S3 board support into IDE, for this first you need to add below link into preference:
     
     ```
     https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
     ```
     
     Select File > Preference, and add link as show in below image,
      <img src= "https://github.com/sbcshop/3.2_Touchsy_ESP-32_Resistive_Software/blob/main/images/preference_board.gif" />
      
   - Now will install ESP32 based boards as shown in below image,

     <img src= "https://github.com/sbcshop/3.2_Touchsy_ESP-32_Resistive_Software/blob/main/images/install_ESP32boards.gif" />
   
   - You have two options to program onboard ESP32 of EnkFi board, **_UART USB_** OR **_Native USB_**.

     <img src="https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/images/usb_options.png" width="372" height="214">   
   
   - When using Native ESP USB, you will have to press BOOT button once and then connect Type C. For UART USB no need, directly connect USB.
   
   - Once done (for UART USB), keeping default settings select the ESP32S3 Dev Module with suitable COM PORT (may be different in your case) as shown below,

     <img src="https://github.com/sbcshop/3.2_Touchsy_ESP-32_Resistive_Software/blob/main/images/select_esp32_with_comport.gif">

     You can view assigned COM port through Device Manager,

     <img src="https://github.com/sbcshop/2x2_Display_ESP32_Software/blob/main/images/UART_com_port.jpg" width="582" height="421">
     
   - When using USB native you will get COM PORT as shown in below image, and while uploading you can enable CDC Mode to visualize data on serial com port.
     
     <img src="https://github.com/sbcshop/2x2_Display_ESP32_Software/blob/main/images/Native_USB_device_com_port.jpg" width="410" height="93">
     
     <img src="https://github.com/sbcshop/2x2_Display_ESP32_Software/blob/main/images/Native_USB_Arduino_com.jpg" width="" height="">
     
        
### 2. Installing Libraries
   - When compiling sample codes there are some dependency on external libraries sometime which you can add as shown here.
   - RTC library for testing DS3231, select Sketch > Include Library > Manage Libraries. Install RTClib version 2.1.4,

     <img src= "https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/images/Lib_install.png" />

     <img src= "https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/images/RTClib_install_1.png" />

   - Similarly you can add more libraries if needed, make sure to install correct version. 


### 3. Testing First Code
   - At this step you are all set to test codes, for easy getting started we have provided various demo [example codes](https://github.com/sbcshop/EnkFi_7.5_Software/tree/main/examples) in github which you can download and try. 
   - Open one example code in Arduino and make sure you have selected correct board with suitable com port, click on upload button to transfer code on EnkFi board.
     <img src="https://github.com/sbcshop/3.2_Touchsy_ESP-32_Resistive_Software/blob/main/images/upload_process.gif">
   - Checkout other examples below and build your own custom program codes using those references.

### Example Codes
   - [Example 1](https://github.com/sbcshop/EnkFi_7.5_Software/tree/main/examples/Demo_Buzzer_Button) : Onboard Button and Buzzer Testing 
   - [Example 2](https://github.com/sbcshop/EnkFi_7.5_Software/tree/main/examples/Demo_GraphicsDisplay) : Create Graphics like line, circle, etc. on EnkFi E-Paper display
   - [Example 3](https://github.com/sbcshop/EnkFi_7.5_Software/tree/main/examples/Demo_ImageDisplay) : Image display demo, follow instructions [here](https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/documents/Image%20to%20Arduino%20Byte%20Conversion.pdf) to create your own array image to use with code.   
   - and [Many more...](https://github.com/sbcshop/EnkFi_7.5_Software/tree/main/examples)

   Now you are ready to try out your own codes, **_Happy Coding!_**

-->
## Resources
  * [Schematic](https://github.com/sbcshop/StackyFi_Hardware/blob/main/Design%20Data/StackyFi%20SCH.pdf)
  * [Hardware Files](https://github.com/sbcshop/StackyFi_Hardware)
  * [Step File](https://github.com/sbcshop/StackyFi_Hardware/blob/main/Mechanical%20Data/StackyFi%20STEP.step)
  * [Getting Started with ESP32 in Arduino](https://docs.espressif.com/projects/arduino-esp32/en/latest/)
  * [ESP32 S3 Hardware Reference](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/hw-reference/index.html)
  * [ESP32 S3 Datasheet](https://github.com/sbcshop/3.2_Touchsy_ESP-32_Capacitive_Software/blob/main/documents/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)
  * [Arduino IDE 1 overview](https://docs.arduino.cc/software/ide-v1/tutorials/Environment)
       

## Related Products  
  
  * [1.28 Round Touch LCD HAT](https://shop.sb-components.co.uk/products/1-28-round-touch-lcd-hat-for-raspberry-pi)

    ![1-28-round-touch-lcd-hat-for-raspberry-pi](https://shop.sb-components.co.uk/cdn/shop/files/shopimages_87b6d1ec-2c95-4621-a07f-5937a8d8c090.png?v=1687857703&width=150)

  * [Power Monitoring HAT](https://shop.sb-components.co.uk/products/power-monitoring-hat)

    ![Power Monitoring HAT](https://shop.sb-components.co.uk/cdn/shop/products/1_7bd8c391-47e4-48e4-ac76-5d49d86f9e71.png?v=1610776295&width=150)

  * [Zero Barcode HAT](https://shop.sb-components.co.uk/products/zero-barcode-hat)

    ![zero-barcode-hat](https://shop.sb-components.co.uk/cdn/shop/products/0.jpg?v=1669181323&width=150)
    
  * [RFID HAT](https://shop.sb-components.co.uk/products/rfid-hat-for-raspberry-pi)

    ![RFID HAT](https://shop.sb-components.co.uk/cdn/shop/products/RFIDforPi.jpg?v=1614587676&width=150)


## Product License

This is ***open source*** product. Kindly check LICENSE.md file for more information.

Please contact support@sb-components.co.uk for technical support.
<p align="center">
  <img width="360" height="100" src="https://cdn.shopify.com/s/files/1/1217/2104/files/Logo_sb_component_3.png?v=1666086771&width=300">
</p>
