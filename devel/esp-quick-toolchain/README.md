# `devel/esp-quick-toolchain`

A tool-chain for [ESP8266/Arduino](https://github.com/esp8266/Arduino).
ESP8266/Arduino does not use the official tool-chain for ESP8266 by espressif.
To build Arduino projects, you need this.

## Status

* `poudriere bulk` succeeds without warning on 14-CURRENT and 13.0-RELEASE
* compiles a blink example for ESP8266 with ESP8266/Arduino version 3.x
* compiles [arendst/Tasmota](https://github.com/arendst/Tasmota) for Arduino
  3.x
* `portlint` complains about `autoconf` and `automake`, but `USES+=autoreconf`
  is not what I need
* Arduino 2.x support has been dropped
  (`RECOMMENDED_ARDUINO_FRAMEWORK_VERSION` in `esphome` is now 3.x). If if you
  really need it, let me know why.

## Usage in `platformio` projects

After install, create symlinks in `~/.platformio/packages`.

```console
mkdir ~/.platformio/packages
cd ~/.platformio/packages
ln -s /usr/local/esp-quick-toolchain-gcc103/xtensa-lx106-elf .
ln -s /usr/local/esp-quick-toolchain-gcc103/mklittlefs .
```

`espressif8266` platform should be version 3.x. The tool-chain and tools
should match the versions in `/usr/local/esp-quick-toolchain-gcc103/xtensa-lx106-elf/.piopm`.

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

As of this writing, `esphome` defaults to Arduino 3.x, which depends on GCC
10.x.

Install `gcc103` `FLAVOR`. Follow the instruction for `platformio`.
