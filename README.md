# StackyFi_Software

<img src= "https://github.com/sbcshop/StackyFi_Software/blob/main/images/StackyFi_main_Banner.png" />
StackyFi is an innovative standalone mini-controller board designed with the Raspberry Pi Zero physical factor and powered by the powerful ESP32-S3 WROOM 1 microcontroller. StackyFi eliminates the requirement for a Raspberry Pi board by effortlessly supporting most Raspberry Pi HATs, allowing you to stack them directly on its tiny frame. The device includes an integrated 6D MEMS IMU, RGB LED, camera integration, and wireless connectivity such as WiFi and Bluetooth® 5 (LE). StackyFi is ideal for your next-generation IoT prototype projects, spanning from smart home applications to security and surveillance systems.

This GitHub provides getting started instructions to use StackyFi board.

### Features
- Powered by ESP32 S3 Wroom-1 microcontroller module
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


## Specification:
- **Microcontroller**  : ESP32-S3 series of SoCs having Xtensa® dual-core 32-bit LX7 microprocessor
- **Connectivity** : 2.4 GHz Wi-Fi (802.11 b/g/n) and Bluetooth® 5 (LE)
- **Memory** : Flash up to 16 MB, PSRAM up to 8 MB
- **Working mode** : Support STA/AP/STA+AP 
- **Board Supply Voltage** : 5V 
- **Operating Pin Voltage** : 3.3V 
- **6D MEMS IMU** : QMI8658 (3-axis accelerometer, 3-axis gyroscope)
- **Battery Connector** : Supports 3.7V Lithium ion battery  
- **RGB LED** : WS2812B
- **Camera Compatible** : OV2640 Camera Module 2MP
- **Additional Storage** : TFcard support
- **Working Temperature** : -20°C ~ +70°C
  
## Getting Started with StackyFi
### Pinout
<img src= "https://github.com/sbcshop/StackyFi_Software/blob/main/images/StackyFi_Pinout.png" />


### Interfacing Details

 - **_SDcard Interface_**

   | ESP32 | SDCard | Function |
   |---|---|---|
   | IO42 | CARD_CLK | Clock pin of SPI interface for Display|
   | IO2  | CARD_MOSI | MOSI (Master OUT Slave IN) pin of SPI interface|
   | IO41 | CARD_MISO  | MISO (Master IN Slave OUT) pin of SPI interface|
   | IO1  | CARD_CS  | Chip Select pin of SPI interface|

- **_RGB LED and Buttons Interfacing_**

  | ESP32 | Hardware | Function |
  |---|---|---| 
  |IO0 | BOOT |Boot button |
  |IO45 | DIN | WS2812B RGB LED|

- **_QMI8658 IMU interfacing with ESP32 using I2C_** 

  | ESP32 | IMU | Description | 
  |---|---|---|
  | IO38 | SDA | I2C Serial Data Pin |
  | IO39 | SCL | I2C Serial Clock Pin |

- **_Camera interfacing with ESP32_** - Following pins consumed when camera connected with StackyFi, 
  | ESP32 | Camera OV2640| Pin Type Function |
  |---|---|---|
  | IO4 | SDA/SIO_D  | SCCB serial interface Data I/O |
  | IO5 | SCL/SIO_C | SCCB serial interface clock input |
  | IO6 | VSYNC | Vertical Synchronization Output |
  | IO7 | HREF | Horizontal Reference Output |
  | IO13 | PCLK   | Pixel Clock Output  |
  | IO15 | XCLK  | System Clock Input |
  | IO16 | Y9 | Video Port Output bit[9] |
  | IO17 | Y8  | Video Port Output bit[8] |
  | IO18 | Y7 | Video Port Output bit[7] |
  | IO12 | Y6   | Video Port Output bit[6] |
  | IO10 | Y5  | Video Port Output bit[5] |
  | IO8 | Y4  | Video Port Output bit[4] |
  | IO9 | Y3 | Video Port Output bit[3] |
  | IO11 | Y2 | Video Port Output bit[2]  |
  
- **_40Pin Standard Header Pin Compare_**: useful when using any Raspberry Pi HAT with StackyFi to decide corresponding GPIOs utilized. Camera and SDcard pins only consumed when connected otherwise free to use as normal GPIOs.

  <img src= "https://github.com/sbcshop/StackyFi_Software/blob/main/images/PINcompare_RPi_StackyFi.png" />

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

     <img src="https://github.com/sbcshop/StackyFi_Software/blob/main/images/usb_options.jpg" width="213" height="118">   
   
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
   - for example installing library for RGB LED and IMU sensor, select Sketch > Include Library > Manage Libraries. Install FastLED version 3.6.0 and SensorLib version 0.1.9,

     <img src= "https://github.com/sbcshop/EnkFi_7.5_Software/blob/main/images/Lib_install.png" />

     <img src= "https://github.com/sbcshop/StackyFi_Software/blob/main/images/fastLED_lib.png" width="583" height="310" />
     <img src= "https://github.com/sbcshop/StackyFi_Software/blob/main/images/sensorlib.png" width="589" height="217" />

   - Similarly you can add more libraries if needed, make sure to install correct version. 


### 3. Testing First Code
   - At this step you are all set to test codes, for easy getting started we have provided various demo [example codes](https://github.com/sbcshop/StackyFi_Software/tree/main/examples) in github which you can download and try. 
   - Open one example code in Arduino and make sure you have selected correct board with suitable com port, click on upload button to transfer code on EnkFi board.
     <img src="https://github.com/sbcshop/StackyFi_Software/blob/main/images/upload_code.gif">
   - Checkout other examples below and build your own custom program codes using those references.

### Example Codes
   - [Example 1](https://github.com/sbcshop/StackyFi_Software/tree/main/examples/Demo_IMU/Demo_IMU.ino) : Onboard IMU QMI8658 Demo to read accelerometer, Gyro and temperature Data.
   - [Example 2](https://github.com/sbcshop/StackyFi_Software/blob/main/examples/RGB_LED_Demo/RGB_LED_Demo.ino) : Play with onboard RGB LED.
   - [Example 3](https://github.com/sbcshop/StackyFi_Software/tree/main/examples/CameraWebServer) : Camera WebServer demo to test OV2640 camera module  
    and more [here](https://github.com/sbcshop/StackyFi_Software/tree/main/examples)

   Now you are ready to try out your own codes, **_Happy Coding!_**

## Resources
  * [Schematic](https://github.com/sbcshop/StackyFi_Hardware/blob/main/Design%20Data/StackyFi%20SCH.pdf)
  * [Hardware Files](https://github.com/sbcshop/StackyFi_Hardware)
  * [Step File](https://github.com/sbcshop/StackyFi_Hardware/blob/main/Mechanical%20Data/StackyFi%20STEP.step)
  * [Getting Started with ESP32 in Arduino](https://docs.espressif.com/projects/arduino-esp32/en/latest/)
  * [ESP32 S3 Hardware Reference](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/hw-reference/index.html)
  * [ESP32 S3 Datasheet](https://github.com/sbcshop/3.2_Touchsy_ESP-32_Capacitive_Software/blob/main/documents/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)
  * [Arduino IDE 1 overview](https://docs.arduino.cc/software/ide-v1/tutorials/Environment)
       

## Related Products  

  * [2 Channel Relay HAT](https://shop.sb-components.co.uk/products/zero-relay-2-channel-5v-relay-board-for-raspberry-pi)

    ![zero-relay-2-channel](https://shop.sb-components.co.uk/cdn/shop/files/1_37.png?v=1727765023&width=150)
  
  * [1.28 Round Touch LCD HAT](https://shop.sb-components.co.uk/products/1-28-round-touch-lcd-hat-for-raspberry-pi)

    ![1-28-round-touch-lcd-hat-for-raspberry-pi](https://shop.sb-components.co.uk/cdn/shop/files/shopimages_87b6d1ec-2c95-4621-a07f-5937a8d8c090.png?v=1687857703&width=150)

  * [Power Monitoring HAT](https://shop.sb-components.co.uk/products/power-monitoring-hat)

    ![Power Monitoring HAT](https://shop.sb-components.co.uk/cdn/shop/products/1_7bd8c391-47e4-48e4-ac76-5d49d86f9e71.png?v=1610776295&width=150)

  * [Zero Barcode HAT](https://shop.sb-components.co.uk/products/zero-barcode-hat)

    ![zero-barcode-hat](https://shop.sb-components.co.uk/cdn/shop/products/0.jpg?v=1669181323&width=150)
    
  * [StackyPi - Powered by Pico RP2040](https://shop.sb-components.co.uk/products/stackypi)

    ![stackypi](https://shop.sb-components.co.uk/cdn/shop/products/StackyPi.png?v=1648531908&width=150)


## Product License

This is ***open source*** product. Kindly check LICENSE.md file for more information.

Please contact support@sb-components.co.uk for technical support.
<p align="center">
  <img width="360" height="100" src="https://cdn.shopify.com/s/files/1/1217/2104/files/Logo_sb_component_3.png?v=1666086771&width=300">
</p>
