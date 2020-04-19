# Customized ESP32 bootloader which initializes External RAM (PSRAM)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This bootloader initializes the External RAM and copies data from flash to RAM if an EXTRAM segment is present in the application binary. (Normally the PSRAM is initialized in the application code and data is not copied automatically.)

(This is helpfull for e.g. developing bare metal Rust applications: https://github.com/esp-rs/esp32-hal).

## Usage
The repository includes a pre-built build/bootloader.bin. This can replace the regular bootloader files build by esp-idf or included in the Arduino builds: https://github.com/espressif/arduino-esp32/tree/master/tools/sdk/bin.

Only a single binary is included as esptool.py can properly set the identification bytes for the different types of supported flashes.

The build/bootloader.bin file needs to be written to address 0x1000 in the flash. For example:
```
esptool.py --port /dev/ttyUSB0 write_flash --flash_mode dio --flash_freq 40m --flash_size detect 0x01000 bootloader.bin
```

The prebuilt version is built in release mode to keep the size down, but does include warning and error level logging.

## Building
If you prefer to build the binary yourself, you need a working copy of the esp-idf v4.0: https://github.com/espressif/esp-idf/tree/v4.0

With this enivronment setup properly you can use `idf.py bootloader` to build and `idf.py bootloader-flash` to flash the bootloader.

## License
Both the original bootloader files and the modifications are licensed under the [Apache 2.0 License](LICENSE)
