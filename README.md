# LE GPS Receiver
LE GPS Receiver is a Bluetooth 4.0 Smart Location & Navigation Service central app dedicated to bond with LNS peripheral app.

Its purpose is to receive the GPS location streamed by the peripheral and expose the received data in a comprehensive way.

TODO link to transmitter

## 1 - Hardware target
This receiver version is dedicated to the **nRF51822** excellent Bluetooth 4.0 Low Energy SoC designed by Nordic. 

TODO link to nRF / Nodric

## 2 - Free firmware
This **free firmware** can run on any nRF51822 with this capabilities:

  * 256 KB of flash.
  * 32 KB of RAM.

Please note that you may find previous revisions of this SoC with 128 KB of Flash or 16 KB of RAM. This firmware may or may not work on it, as it is untested for the moment. 

Specially designed for happy hobbyists, this version has been tested and runs on the RedbearLab Nano board v1.5. (v1.0 has only 16KB of RAM, it might work, but I've didn't try).

TODO ReadbearLab logo, link, image?

The Nano board is based on the MDBT40 from Raytac. So if you use this submodule, it will work too. 

### 2.1 - Pairing
The pairing with LE GPS transmitter is really easy and automatic. Turn on LE GPS or any other standard LNS capable device.

Turn on your nRF51822 board. LE GPS Receiver firmware boots up and starts to scan for a GPS. Once LNS found it tries to pair and bound. You might need to accept on the GPS side the pairing process. Then the receiver starts to get GPS data and produces the ouptput.

### 2.2 - Output
This free version will ouptut data to the **UART**:

* 38200 BAUD rate
* 8n1
* No flow controll

This allows you to directly get bytes on an Arduino or a Raspberry Pi for example.

Please note that the UART I/O are **3.3v only!** Raspberry Pi is ok, Arduino are mostly 5v, so it needs a level adapter.

### 2.3 - Sentences
Once the UART connected and LE GPS bonded, you'll receive a stream of ASCII bytes.

For easy parsing, each line is terminated by \r\n characters (0x0A 0x0D).

The data sentences start with a $ character and data are comma ( , ) separated.

#### Boot header
When the device is powered up, it shows this header


```
***********************************

***********************************
```


#### Position
Once the GPS send a valid position, you'll receive this sentence:

```
$LEGPS-POS,48.898048,N,2.286839,E,31.6
```
The construction of the sentence is $LEGPS-POS,1,2,3,4,5 where:

1. Latitude in degrees
2. N for north, S for south
3. Longitude in degrees
4. E for East, W for West
5. Altitude in meters

#### Time
If the GPS send a valid time, you'll receive this sentence:

```
$LEGPS-UTC,2015,11,21,23,11,14
```
The construction of the sentence is $LEGPS-UTC,1,2,3,4,5,6 where:

1. Year YYYY
2. Month MM from 1 to 12
3. Day DD from 1 to 31
4. Hours HH from 1 to 23
5. Minutes MM from 1 to 59
6. Seconds SS from 1 to 59

#### Movement
If the GPS send heading or speed, you'll receive this sentence:

```
$LEGPS-MOV,2.3,355.8
```
The construction of the sentence is $LEGPS-MOV,1,2 where:

1. Speed in meters/second
2. Heading from 0 to 360 in degrees

#### Battery
If the GPS send its battery level, you'll receive this sentence:

```
$LEGPS-BAT,98
```
The construction of the sentence is $LEGPS-BAT,1 where:

1. Battery level over 100 (as in %)

## 3 - PRO firmware
As a freelance I offer my services to create a professional version of this firmware with many upgraded features. I can also add specific and custom features.

Feel free to contact me for any requests.

### 3.1 - SoC support
I can build a specific firmware for 128KB of flash and 16KB of RAM

### 3.2 - Output
You can get a specific firmware with SPI support.

You can get UART flow control, multiple Baud rate support.

### 3.3 - Sentences
Get professionnal NMEA output to feed a standard GPS data parser.










