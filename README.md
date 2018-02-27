**IMPORTANT NOTE:**

 This is a slightly modified copy of MrBuddyCasino's ESP32\_MP3\_Decoder project. The code and this README doc has been modified to make the project set up compatible with the Embedded Adventures WRL-4001 Audio Development Board

ESP32 Web Radio
=======================
This is a simple web radio streamer. It connects to a web radio station via wifi, decodes the stream and plays the sound via I2S codec or
to a speaker directly connected to the DAC pins.

Features:

* Decodes MP3 and AAC (Beta)
* Bluetooth Speaker mode

## Required Software

Get the SDK:

    git clone https://github.com/espressif/esp-idf.git
    cd esp-idf
    git submodule update --init

Set the IDF_PATH environment variable, and point it to this directory.

    export IDF_PATH=/path/to/esp-idf

Download the toolchain from: https://github.com/espressif/esp-idf#setting-up-esp-idf
You will need version 5.2.0.
Add /path/to/xtensa-esp32-elf/bin to your PATH:

    export PATH=/path/to/xtensa-esp32-elf/bin:$PATH

## Configuration

The serial port and wifi credentials are configured using make.
Type `make menuconfig` and 

* configure your serial port in `Serial flasher config` submenu
* select `Web Radio / Bluetooth Speaker` submenu
  * configure wifi credentials
  * select audio output mode
  * activate / disable bt speaker mode
* 'save', then exit

You can edit the list of radio stations in the `/main/playlist.pls` playlist file.

## Building
If this is the first time, initialize the submodules:
`git submodule init && git submodule update`.
Then, just type `make all`.

## Flashing
Connect your serial cable and run 'make flash'. To see serial console output run 'make monitor'.

## Controls
There is an option to connect a pushbutton to the WRL-4001 board, to GPIO4. This button allows you to advance to the next track in the playlist.

## Bluetooth Speaker Mode

Enable `Classic Bluetooth` in `Component config > Bluetooth > Bluedroid Bluetooth stack enabled > Classic Bluetooth`, enable `A2DP > A2DP ROLE config (SINK)`, then enable `Bluetooth Speaker Mode` via `make menuconfig`. After flashing, you should see a Bluetooth device called "ESP_SPEAKER". If you don't like that name, you can change it via menuconfig.


## Known Issues

* Some AAC streams may not be playable

## More Information

There is a thread over at the ESP32 forum:
https://esp32.com/viewtopic.php?f=17&t=1026
