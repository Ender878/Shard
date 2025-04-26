# Shard - Custom ESP32 S3 Board :electron:

![Shard_png2](https://github.com/user-attachments/assets/2b6138d2-c1b5-407c-aaca-fd7eff1a97fd)

**Shard** is an open source **ESP32 S3** board that I designed as a summer project to learn more about electronics and PCB design.

## Core features:

- 16MB Flash
- WiFi and Bluethoot capabilities
- Built-in Neopixel RGB LED
- 21 configurable GPIO pins
- Up to 16V for external Power supply
- UART & Configurable SPI and I2C pins

The board itself is pretty small, 4.6x4.8cm and doesn't have mounting holes unfortunately. It is designed to be an all-feature development board for prototyping.

## Programming

### Uploading

The board doesn't come with a **USB-UART bridge**, so the firmware uploading requires user input:

- When the uploading process starts, hold the **RESET** button
- Immediately after you pressed it, press the **BOOT** button and then release the **RESET** button
- After the code is uploaded, press the **RESET** button again to exit Download Mode, so that the board can execute the code.

### Programming with Arduino IDE 2

To program this board with the **Arduino IDE**, you have to:
- Install the "esp32" board manager.
- then select the **UM-PROS3** board 
- when uploading, follow the steps listed in the **[Uploading](#uploading)** section.

### Programming with PlatformIO (recommended)

To program this board with **PlatformIO**, you should configure the **platformio.ini** file as follows:

~~~ini
[env:esp32-s3-devkitc-1]
platform = espressif32
board = shard
framework = arduino
~~~

I made a custom **board** config file for PlatformIO that specifies all the board's specifications. To use it, create a folder called **boards** and copy [this file](./shard.json) under it.

Also, this is the partition I used:

~~~csv
# Name,   Type, SubType, Offset,  Size, Flags
nvs,      data, nvs,     0x9000,  0x5000,
otadata,  data, ota,     0xe000,  0x2000,
app0,     app,  ota_0,   0x10000, 0x700000,
app1,     app,  ota_1,   0x710000,0x700000,
spiffs,   data, spiffs,  0xe10000,0x1F0000,
~~~

PlatformIO should find the board automatically. When uploading, still follow the steps in the **[Uploading](#uploading)** section.

## Reference

To design this board, I mainly referred to the Espressif's [ESP32-S3 Hardware Design Guidelines](https://docs.espressif.com/projects/esp-hardware-design-guidelines/en/latest/esp32s3/esp-hardware-design-guidelines-en-master-esp32s3.pdf).
