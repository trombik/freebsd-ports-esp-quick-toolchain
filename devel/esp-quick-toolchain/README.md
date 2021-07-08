# `devel/esp-quick-toolchain`

A tool-chain for [ESP8266/Arduino](https://github.com/esp8266/Arduino).
ESP8266/Arduino does not use the official tool-chain for ESP8266 by espressif.
To build Arduino projects, you need this.

## Status

* `poudriere bulk` succeeds without warning on 14-CURRENT and 13.0-RELEASE
* compiles a blink example for ESP8266 with ESP8266/Arduino version 3.0.0
* compiles [arendst/Tasmota](https://github.com/arendst/Tasmota) for Arduino
  3.0.0
* `portlint` complains about `autoconf` and `automake`, but `USES+=autoreconf`
  is not what I need
* `gcc48` `FLAVOR` compiles projects for ESP8266/Arduino version 2.x

## Usage in `platformio` projects

After install, create symlinks in `~/.platformio/packages`.

```console
mkdir ~/.platformio/packages
cd ~/.platformio/packages
ln -s /usr/local/esp-quick-toolchain-gcc102/xtensa-lx106-elf .
ln -s /usr/local/esp-quick-toolchain-gcc102/mklittlefs .
```

`espressif8266` platform should be version 3.0.0. The tool-chain and tools
should match the versions in `/usr/local/esp-quick-toolchain-gcc102/xtensa-lx106-elf/.piopm`.

`platformio.ini` should look like this:

```ini
platform = espressif8266 @ 3.0.0
framework = arduino
platform_packages = toolchain-xtensa @ 5.100200.210605
 tool-mklittlefs @ 5.100200.210605
board = d1_mini
```

Then, run `pio run` in the project directory.

### Usage in `esphome`

As of this writing, `esphome` defaults to Arduino 2.x, which depends on GCC 4.8.

Install `gcc48` `FLAVOR`. Follow the instruction for `platformio`.

```console
> esphome run livingroom.yaml
INFO Reading configuration livingroom.yaml...
INFO Generating C++ source...
INFO Compiling app...
INFO Running:  platformio run -d foo
Processing foo (board: nodemcuv2; framework: arduino; platform: platformio/espressif8266@2.6.2)
--------------------------------------------------------------------------------------------------------------------------------------
HARDWARE: ESP8266 80MHz, 80KB RAM, 4MB Flash
PACKAGES:
 - framework-arduinoespressif8266 3.20704.0 (2.7.4)
 - tool-esptool 1.409.0 (4.9)
 - tool-esptoolpy 1.20800.0 (2.8.0)
 - tool-mklittlefs 5.100200.210605 (10.2.0)
 - toolchain-xtensa 2.40802.200502 (4.8.2)
Library Manager: Installing Update
Library Manager: Already installed, built-in library
Dependency Graph
|-- <ESPAsyncTCP-esphome> 1.2.3
|   |-- <ESP8266WiFi> 1.0
|-- <ESPAsyncWebServer-esphome> 1.2.7
|   |-- <ESPAsyncTCP-esphome> 1.2.3
|   |   |-- <ESP8266WiFi> 1.0
|   |-- <Hash> 1.0
|   |-- <ESP8266WiFi> 1.0
|-- <ESP8266WiFi> 1.0
|-- <ESP8266mDNS> 1.2
|   |-- <ESP8266WiFi> 1.0
|-- <DNSServer> 1.1.1
|   |-- <ESP8266WiFi> 1.0
Compiling .pioenvs/foo/src/esphome/components/api/api_connection.cpp.o
Compiling .pioenvs/foo/src/esphome/components/api/api_pb2.cpp.o
Compiling .pioenvs/foo/src/esphome/components/api/api_pb2_service.cpp.o
Compiling .pioenvs/foo/src/esphome/components/api/api_server.cpp.o
...
```
