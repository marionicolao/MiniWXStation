# MiniWX Station
ESP8266 IoT and BME280 sensor for a minimalistic weather station to put in your terrace :-)

This work started as a fork from F4GOH code, so you can visit his blog (https://hamprojects.wordpress.com/) for infos about
how to compile and configure this firmware trough his menu. This instead is his github repository: https://github.com/f4goh/Weather. I've added some features that, at moment, you can set at compile time using #defines.
Many thanks to Antonio EA1CDV for his support, beta testing and encouragement, you can read a detailed article in spanish language about this project in his blog: http://ea1cdv.blogspot.com/2018/08/estacion-meteorologica-aprs-via-wifi.html
In a next version i'll change the source code to use native ESP8266 ntp calls instead of using NTPTimeESP, but for the moment the source code needs this library, so you have to add it to your environment, https://github.com/SensorsIot/NTPtimeESP
Obviously you nedd the BME280 Library too: https://github.com/sparkfun/SparkFun_BME280_Arduino_Library

For the moment this project is running without problems over three flavours of ESP8266:
- NodeMCU V0.9  (ESP-12)
- NodeMCU V1.0  (ESP-12E)
- Wemos D1 mini (ESP-12F)


```javascript
//**** How the station is named in your NET
const char* WiFi_hostname = "IU5HKU-13";
```
Change with the name you wish.

```javascript
//**** APRS PASSWORD (use -1 if you are using a CWOP callsign)
const char* AprsPassw = "YourAprsNumericalPASS";
```
For a CWOP callsign you need to register, it's free and easy, refer to
instruction at http://wxqa.com/ to obtain one.

```javascript
//**** comment this for hardcoded 3.7V value in telemetry
#define HAVE_BATTERY
```

This is for reading analog values connected to A0, for the proper value of the resistor to put in series
refer to this thread: https://forum.arduino.cc/index.php?topic=445538.0

```javascript
//**** uncomment this for weatherunderground upload,remember to set ID and PASSWORD of your account
#define USE_WUNDER
//* change ID and PASSWORD with yours
char ID [] = "YourWunderID";                      
char PASSWORD [] = "YourWunderPASSW";
```

Major upgrade, sends data to Weahter Underground.

```javascript
//**** show BME280 registers in printbme();
//#define DISPLAY_BME_REGS
```

Uncomment for printout of registers values in serial console.

```javascript
//**** blinking led to show that into the 10 minutes the system is still alive (1" blink)
#define BLINK_RED_LED
```

WILL BE ELIMINATED IN BATTERY POWERED VERSION, this is a "i'm still alive" indication.

```javascript
//**** blinking led to show that ESP8266 is transmitting  (0.5" blink)
#define BLINK_BLUE_LED
```

WILL BE ELIMINATED IN BATTERY POWERED VERSION, this is a "i'm sending data to servers" indication.

```javascript
//**** show (annoying) animated clock in the serial output 
//#define SHOW_TICKS
```

Left commented to eliminate the clock in serial console.

```javascript
//**** use static ip instead of dns one
//#define USE_STATIC_IP
//* change to reflect your net configuration
#ifdef USE_STATIC_IP
String stat_ip="192.168.0.200";        // STATIC IP
String stat_gateway="192.168.0.1";     // GATEWAY
String stat_subnet="255.255.225.0";    // SUBNET MASK
String stat_dns1="8.8.8.8";            // DNS1
String stat_dns2="4.4.2.2";            // DNS2
IPAddress ip,gateway,subnet,dns1,dns2;
#endif
```

Self explanatory, this settings are needed if you want a static ip for the station.

If you are using ArduinoIDE for development, then you can choose between some linkage options, one of the most important is the "lwIP" one:



More detail about this funny project will follow ASAP.
