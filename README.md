# loboris backports
A list of suggested features that could be imported from the loboris ESP32 MicroPython fork into mainline MicroPython.

## Motivation

A couple of years ago Boris Lovosevic [cloned the MicroPython repository](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo) and added many features specifically tailored for the Espressif ESP32 microcontroller ([see them listed in his wiki](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki)). 

Developers adopted this code and have used it to successfully build applications. As time passed Boris appears to have moved on to other interests and his repository is dormant. There is interest in preserving the more valuable features of his project by importing them into mainstream MicroPython.

It was suggested that a list of features be assembled that could be evaluated and discussed. This markdown file is offered as a convenient starting point for the list. If you are interested in contributing, please clone this repository, add your suggestions, and offer pull requests. Or if you prefer, merely post your suggestions as an 'issue' and they may be incorporated.

## Major Aspects of the loboris repository

* [The build system](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/build)

  The loboris repository contains everything you need to build firmware that can be burned onto an ESP32 board. It includes the very sizeable Xtensa toolchains and esp-idf, [a build script](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/build) with many useful options including the ability to make and flash both firmware and a filesystem with contents, and a menuconfig setup that lets you conveniently view and set dozens of options. 

* [The network module](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/network)

  This includes an optional FTP server that will run on the ESP32, a telnet server, [an SSH server](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/ssh), a Mqtt client, curl, etc. It also exposes enhanced WiFi capabilities with better status reporting and event generation in the case of disconnection.

* [OTA update capability](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/ota)

  You can update your firmware over the internet.

* [The machine module](https://github.com/loboris/MicroPython_ESP32_psRAM_LoBo/wiki/machine)

  Many enhancements to the machine class including the exposing of reset and wakeup reasons, manipulating the watchdog timer, non-volatile storage, and logging.

* Enhanced access to peripherals

  Many improved classes giving more granular access to ADC, PWM, I2C, UART, SPI, RTC, the Pin class, etc.