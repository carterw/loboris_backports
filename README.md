# loboris backports
A list of suggested features that could be imported from the loboris ESP32 MicroPython fork into mainline MicroPython.

## Motivation

A couple of years ago Boris Lovosevic [cloned the MicroPython repository](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo) and added many features specifically tailored for the Espressif ESP32 microcontroller ([see them listed in his wiki](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki)). 

Developers adopted this code and have used it to successfully build applications. As time passed Boris appears to have moved on to other pursuits and his repository is dormant. There is interest in preserving the more valuable features of his project by importing them into mainstream MicroPython.

It was suggested that a list of features be assembled that could be evaluated and discussed. This markdown file is offered as a convenient starting point for the list. If you are interested in contributing, please clone this repository, add your suggestions, and offer pull requests. Or if you prefer, merely post your suggestions as an 'issue' and they may be incorporated.

## Major Aspects of the loboris repository

* [The build system](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/build)

  The loboris repository contains everything you need to build firmware that can be burned onto an ESP32 board. It includes the very sizeable Xtensa toolchains and esp-idf, esptool, [a build script](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/build) with many useful options including the ability to make and flash both firmware and a filesystem with pre-loaded contents, and a menuconfig implementation that lets you conveniently view and set dozens of options. 

* [The network module](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/network)

  This includes an optional FTP server that will run on the ESP32, a telnet server, [an SSH server](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/ssh), a Mqtt client, curl, etc. It also exposes enhanced WiFi capabilities with better status reporting and event generation in the case of disconnection.

* [OTA update capability](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/ota)

  You can update your firmware over the internet. This involves running an http client on the target device that pulls down new images and flashes them locally. 

* [The machine module](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/machine)

  Many enhancements to the machine class including the exposing of reset and wakeup reasons, manipulating the watchdog timer, non-volatile storage, and logging.

* Enhanced access to peripherals

  Many improved classes giving more granular access to ADC, PWM, I2C, UART, SPI, RTC, the Pin class, etc.

# Valuable features

## PWM

The [PWM implementation of MicroPython](https://docs.micropython.org/en/latest/esp32/quickref.html#pwm-pulse-width-modulation) appears to assign the same frequency to all pins. The [loboris implementation](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/pwm) provides for 4 frequency timers and 8 channels, multiple channels can use the same timer. Duty cycles can be assigned independently. Also there is a PWM.list()  function which shows status of all active PWM.

## ADC

The ADC implementation of MicroPython is [described here](https://docs.micropython.org/en/latest/esp32/quickref.html#adc-analog-to-digital-conversion), the loboris implementation is [documented here](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/adc). The loboris port adds access to ADC2 via the 'unit' parameter. Also added are *deinit()* (frees the pin for other purposes) and *vref()* (set up a reference voltage) methods. A set of handy convenience methods are implemented for periodically collecting ADC data as a separate task.

## Filesystems

The loboris port allows for [three different possible filesystem types](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/filesystems); FatFSs (microsoft filesystem?), SPIFF, and LittleFS. These can all be imaged and flashed from the build script.


## Thread support

Mainstream MicroPython uses a [multiple-task technique called asyncio](https://github.com/micropython/micropython-lib/tree/master/uasyncio). In the loboris port a [thread mechanism was implemented](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/thread) which seems very handy. Maybe both could be available in mainstream MicroPython.