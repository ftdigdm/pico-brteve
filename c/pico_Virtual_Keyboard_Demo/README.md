# pico Virtual Keyboard Demo

This is a virtual touchscreen keyboard. It is rendered on the EVE display using the pico MCU to present a HID device on the USB interface to a host. The host treats the output of the pico virtual keyboard as it would a real physical keyboard.

It is straight forward to add multiple screens of keys. An example page showing an additional numeric keypad is enabled. This can be extended in code for other specialist inputs or even macros.

The default layout is UK, although US and DE layouts can be selected from the options screen (cog icon).

![Keyboard Screenshot](./keyboard.jpg)

The code is based on the [BRT_AN_025 Example Code](https://github.com/Bridgetek/EVE-MCU-BRT_AN_025-Example-Pico) library and the [BRT_AN_012 Example Code](https://github.com/Bridgetek/EVE-MCU-BRT_AN_012-Example-Pico).

## Options

By default the project will build for the BT817 as used in the IDM2040-7A module. To change this alter the FT8XX_TYPE in the CMakeLists.txt file.

```
# Modify these to set the target GPU and display
set(FT8XX_TYPE BT817)
set(DISPLAY_RES WVGA)
```

## Screenshots

A screenshot can be taken by defining the ENABLE_SCREENSHOT macro. To take a screenshot click on the "Bridgetek Logo".

The screenshot sends the data from the screen to the stdio port as a binary stream. The program will pause for up-to a minute to allow the data to be sent. It can be captured with a terminal emulator. The data is in the format ARGB4 and is bookended by the string "ARGB start\n" and "ARGB end\n". These must be stripped from the file before use to leave the binary data only.

To convert the screenshot from the ARGB4 format to JPG the following command can be used within Imagemagick to make the conversion:
```
magick.exe convert -size 800x480 -depth 4 -color-matrix "0 0 0 0 1, 1 0 0 0 0, 0 1 0 0 0, 0 0 0 0 0, 0 0 0 0 0" -background black rgba:screenshot.argb screenshot.jpg
```
