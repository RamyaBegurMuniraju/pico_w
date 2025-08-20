
Step 1: Download the Pico SDK
==============================

Clone the official Raspberry Pi Pico SDK and initialize its submodules:

git clone -b master https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
git submodule update --init

Step 2: Set Up Your Project Structure
=====================================

Create a standalone directory for your project:

mkdir ~/standalone
cd ~/standalone


Copy the common config files into it:

cp btstack_config_common.h CMakeLists.txt lwipopts.h .

➤ Client Directory:
mkdir ~/standalone/client
cp btstack_config.h client.c CMakeLists.txt ~/standalone/client/

➤ Server Directory:
mkdir ~/standalone/server
cp btstack_config.h server.c CMakeLists.txt temp_sensor.gatt ~/standalone/server/

Step 3: Set Environment Variable
=================================

Tell CMake where to find the Pico SDK:

export PICO_SDK_PATH=~/pico-sdk


You can also add this line to your ~/.bashrc to make it persistent.

Step 4: Build the Firmware
==========================

Create a build directory and compile the project:

mkdir build
cd build
cmake .. -DPICO_BOARD=pico_w
make -j4


After a successful build, you’ll get a .uf2 firmware file, e.g.:

pico_ble_i2c_slave.uf2


or

picow_ble_temp_sensor.uf2

Step 5: Flash the Pico W via Drag-and-Drop
==========================================

Hold the BOOTSEL button on the Pico W.

Plug in the USB cable while still holding the button.

Release the button once connected — your Pico W will appear as a USB mass storage device named RPI-RP2.

Drag and drop the .uf2 file (e.g. picow_ble_temp_sensor.uf2) onto the drive.

The device will automatically reboot and start running your code.

Step 6: Verify BLE Advertising
==============================

To check that your Pico W is advertising correctly:

Open the nRF Connect app on your smartphone.

Start a BLE scan.

You should see a device with a name like Pico 00:00:00:00:00:00.

Tap on it to explore the advertised services and temperature characteristic.

Check advertisements in Nrf application on phone 



