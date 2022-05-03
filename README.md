# MakeCode Maker [![Actions Status](https://github.com/microsoft/pxt-maker/workflows/pxt-buildtarget/badge.svg)](https://github.com/microsoft/pxt-maker/actions)

-Irshad

The pxt-maker repo is stripped off to target raspbery pi pico 

- Libs are removed from original repo


## Who is this for?

This editor is meant for micro-controllers that are friendly to breadboarding. The editor is based on [Microsoft MakeCode](https://makecode.com).

## Local Dev Server

The local server lets you to run the editor and serve the documentation from your own computer.

### Setup

1. Install [Node.js](https://nodejs.org/) 8.9.4 or higher.
2. Install [Docker](https://www.docker.com/) if you are going to edit any `.cpp` files.
3. Clone the pxt repository.
```
git clone https://github.com/microsoft/pxt
cd pxt
```
4. Install the dependencies of ``Microsoft/pxt`` and build it
```
npm install
npm run build
cd ..
```
5. Clone the ``Microsoft/pxt-common-packages`` repository
```
git clone https://github.com/microsoft/pxt-common-packages
cd pxt-common-packages
npm install
cd ..
```
6. Clone the ``Microsoft/pxt-maker`` repository
```
git clone https://github.com/microsoft/pxt-maker
cd pxt-maker
```
7. Install the PXT command line (add `sudo` for Mac/Linux shells).
```
npm install -g pxt
```
8. Install the pxt-maker dependencies.
```
npm install
```
8. Link pxt-maker back to base pxt repo (add `sudo` for Mac/Linux shells).
```
rm -Rf node_modules/pxt-core
rm -Rf node_modules/pxt-common-packages
pxt link ../pxt
pxt link ../pxt-common-packages
```

If you want to know if your folders are link, run ``ls -l``
and it will indicate them.

```
ls -l node_modules/
```

Note the above command assumes the folder structure of   
```
       maker.makecode.com
          |
  ----------------------------------
  |       |                        |
 pxt      pxt-common-packages  pxt-maker
 ```

### Refresh dal.d.ts files

Whenever you make changes to the ``#defines`` in the .cpp files, you will have to refresh
the ``dal.d.ts`` files. For that, run

```
pxt builddaldts
```

### CODAL changes

If you need to do changes to CODAL itself, follow these steps.

* create a new project in the web editor, then close the web server. Select the hardware you want to work with.
* using a command prompt, open the ``projects`` folder and find the subfolder with your new project
* open the folder in Visual Studio Code
```
code .
```
* open ``pxt.json`` and edit the dependencies to use 
the ``file:...`` path instead of ``*``

```
   dependencies: {
        "adafruit-metro-m0-express": "file:../../libs/adafruit-metro-m0-express"
   }
```
* from the command line, set the ``PXT_NODOCKER`` environment variable to ``1``

```
export PXT_NODOCKER=1
```

* run a local build that will create a CODAL checkout automatically. 
If you are missing tools, you will be notified by the build script.

```
pxt build --local --force
```

* go to the ``built/dockercodal`` folder and open all CODAL in a new Visual Studio Code instance

```
cd built/dockercodal
code libraries/*
```

* go to the Git tab in VS Code, and change the branch of the CODAL repository to work on to ``master``. You can create a new branch to start doing your work and pull requests.

* to build CODAL directly, run ``built/codal``
```
python build.py
```

* to rebuild your project from pxt, run ``pxt build --local --force`` from the project folder

### Running

Run this command from inside pxt-maker to open a local web server
```
pxt serve
```
If the local server opens in the wrong browser, make sure to copy the URL containing the local token. 
Otherwise, the editor will not be able to load the projects.

If you need to modify the `.cpp` files (and have installed yotta), enable yotta compilation using the `--localbuild` flag:
```
pxt serve --localbuild
```

## Repos 

The pxt-maker target depends on several other repos. The main ones are:
- https://github.com/microsoft/pxt, the PXT framework
- https://github.com/microsoft/pxt-commmon-packages, common APIs accross various MakeCode editors
- https://github.com/lancaster-university/codal-core, CODAL core project
- https://github.com/lancaster-university/codal-mbed, mbed layer
- https://github.com/lancaster-university/codal-samd21, CODAL SAMD21 layer
- https://github.com/lancaster-university/codal-circuit-playground, Adafruit CPX layer

## CODAL on local machine

Microsoft Windows [Version 10.0.19042.1645]
(c) Microsoft Corporation. All rights reserved.
```c

D:\makecode\pxt_pico>pxt buildtarget --local
Using target maker with build engine codal
  target: v D:\makecode\pxt_pico
  pxt-core: v D:\makecode\pxt_pico\node_modules\pxt-core
log strings: 24 files; 0 strings -> sim-strings.json
copying common-sim...
D:/makecode/pxt_pico/node_modules/@types/node/index.d.ts(35,1): error TS1084: Invalid 'reference' directive syntax.
D:/makecode/pxt_pico/node_modules/@types/node/index.d.ts(43,30): error TS1005: '=' expected.
D:/makecode/pxt_pico/node_modules/@types/node/index.d.ts(46,30): error TS1005: '=' expected.
D:/makecode/pxt_pico/sim/dalboard.ts(174,87): error TS1109: Expression expected.
D:/makecode/pxt_pico/sim/dalboard.ts(174,93): error TS1109: Expression expected.
D:/makecode/pxt_pico/sim/dalboard.ts(174,126): error TS1005: ':' expected.
building target.json in D:\makecode\pxt_pico...
building D:\makecode\pxt_pico\libs\base
building D:\makecode\pxt_pico\libs\buttons
building D:\makecode\pxt_pico\libs\core
building D:\makecode\pxt_pico\libs\core---rp2040
building D:\makecode\pxt_pico\libs\mixer
building D:\makecode\pxt_pico\libs\mixer---rp2040
building D:\makecode\pxt_pico\libs\rpi-pico
building D:\makecode\pxt_pico\libs\settings
building D:\makecode\pxt_pico\libs\settings---files
building bundled libs/base
building bundled libs/buttons
building bundled libs/core
building bundled libs/core---rp2040
building bundled libs/mixer
building bundled libs/mixer---rp2040
building bundled libs/rpi-pico
[run] git clone https://github.com/lancaster-university/codal built/dockercodal
Cloning into 'built/dockercodal'...
remote: Enumerating objects: 2999, done.
remote: Counting objects: 100% (94/94), done.
remote: Compressing objects: 100% (46/46), done.
remote: Total 2999 (delta 51), reused 81 (delta 48), pack-reused 2905
Receiving objects: 100% (2999/2999), 1.38 MiB | 3.50 MiB/s, done.
Resolving deltas: 100% (1966/1966), done.
[run] cd built/dockercodal; git checkout v0.9.0
Note: switching to 'v0.9.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; git checkout v0.9.0
HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; git checkout v0.9.0
HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; docker run --rm -v D:\makecode\pxt_pico\libs\rpi-pico/built/dockercodal/:/src -w /src -u build pext/arm:gcc9 python build.py
Unable to find image 'pext/arm:gcc9' locally
gcc9: Pulling from pext/arm
d7e10407b4d9: Pull complete
ad563a2293d6: Pull complete
9098e33199ab: Pull complete
d37b1c185edb: Pull complete
85f3e41e22aa: Pull complete
549f9043b418: Pull complete
bb21523d22db: Pull complete
240db6afcd93: Pull complete
Digest: sha256:7c62e88a7c77743908b7b522ded5a0c5007e295dbc0812211cba6063dde69052
Status: Downloaded newer image for pext/arm:gcc9
Creating libraries folder
Cloning into: https://github.com/lancaster-university/codal-pi-pico
Cloning into 'codal-pi-pico'...
Checking out branch: v0.0.10
HEAD is now at 3c5ca9d Snapshot v0.0.10
Set target: codal-pi-pico
Using target-locked.json
Targeting codal-pi-pico
-- The C compiler identification is GNU 9.2.1
-- The CXX compiler identification is GNU 9.2.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/arm-none-eabi-gcc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/arm-none-eabi-g++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
Supressing -Wexpansion-to-defined.
Installing dependencies...
-- Adding library path: (/src/libraries)
Cloning into: https://github.com/lancaster-university/codal-core
Cloning into 'codal-core'...
Checking out branch: b4f03c524dee721c08fbc40f2cd3e9e0c91c6d21
HEAD is now at b4f03c5 fix subclass/protocol for hidjoystick
Cloning into: https://github.com/lancaster-university/codal-rp2040
Cloning into 'codal-rp2040'...
Submodule 'pico-sdk' (https://github.com/mmoskal/pico-sdk) registered for path 'pico-sdk'
Cloning into '/src/libraries/codal-rp2040/pico-sdk'...
Submodule path 'pico-sdk': checked out 'acf638acd7dca45316d704f916605871db9685fc'
Checking out branch: 8590ef14a3d2c11838795ad8b19f1920700b86a6
HEAD is now at 8590ef1 Avoid pin glitch in setDigitial
Synchronizing submodule url for 'pico-sdk'
Using library: codal-pi-pico
Using library: codal-core
Using library: codal-rp2040
-- Found Python3: /usr/bin/python3.9 (found version "3.9.5") found components: Interpreter
CMake Warning at libraries/codal-rp2040/pico-sdk/src/rp2_common/tinyusb/CMakeLists.txt:10 (message):
  TinyUSB submodule has not been initialized; USB support will be unavailable

  hint: try 'git submodule update --init' from your SDK directory
  (/src/libraries/codal-rp2040/pico-sdk).


 /src/libraries/codal-rp2040/inc
-- Configuring done
-- Generating done
-- Build files have been written to: /src/build
make[1]: Warning: File 'CMakeFiles/Makefile2' has modification time 1.1 s in the future
Scanning dependencies of target pre-process-task
[  1%] Executing pre process command
Scanning dependencies of target bs2_default
make[2]: Warning: File 'libraries/codal-rp2040/pico-sdk/src/rp2_common/boot_stage2/CMakeFiles/bs2_default.dir/depend.make' has modification time 1.5 s in the future
[  1%] Building ASM object libraries/codal-rp2040/pico-sdk/src/rp2_common/boot_stage2/CMakeFiles/bs2_default.dir/compile_time_choice.S.o
[  2%] Linking ASM executable ../../../../../../bs2_default.elf
-- The C compiler identification is GNU 10.3.0
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[  2%] Built target bs2_default
Scanning dependencies of target bs2_default_padded_checksummed_asm
make[2]: Warning: File 'bs2_default.elf' has modification time 1.4 s in the future
[  3%] Generating bs2_default.bin
[  3%] Generating bs2_default_padded_checksummed.S
-- The CXX compiler identification is GNU 10.3.0
-- Detecting C compiler ABI info
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[  3%] Built target bs2_default_padded_checksummed_asm
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /src/libraries/codal-rp2040/pico-sdk/tools/elf2uf2/build
make[3]: warning: -j10 forced in submake: resetting jobserver mode.
make[3]: Warning: File 'Makefile' has modification time 1.5 s in the future
make[4]: Warning: File 'CMakeFiles/Makefile2' has modification time 1.5 s in the future
make[5]: Warning: File 'CMakeFiles/elf2uf2.dir/flags.make' has modification time 1.4 s in the future
Scanning dependencies of target elf2uf2
make[5]: warning:  Clock skew detected.  Your build may be incomplete.
make[5]: Warning: File 'CMakeFiles/elf2uf2.dir/flags.make' has modification time 1.3 s in the future
[ 50%] Building CXX object CMakeFiles/elf2uf2.dir/main.cpp.o
[100%] Linking CXX executable elf2uf2
make[5]: warning:  Clock skew detected.  Your build may be incomplete.
[100%] Built target elf2uf2
make[4]: warning:  Clock skew detected.  Your build may be incomplete.
make[3]: warning:  Clock skew detected.  Your build may be incomplete.
/src
[  3%] Built target pre-process-task
Scanning dependencies of target codal-core
make[2]: Warning: File 'libraries/codal-core/CMakeFiles/codal-core.dir/depend.make' has modification time 1.5 s in the future
[  3%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalCompat.cpp.o
[  3%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalComponent.cpp.o
[  4%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalDmesg.cpp.o
[  4%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalFiber.cpp.o
[  4%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalDevice.cpp.o
[  5%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalListener.cpp.o
[  5%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalHeapAllocator.cpp.o
[  6%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalUtil.cpp.o
[  6%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/MemberFunctionCallback.cpp.o
[  6%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/codal_default_target_hal.cpp.o
[  7%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/AbstractButton.cpp.o
[  7%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Accelerometer.cpp.o
[  7%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/CodalUSB.cpp.o
[  8%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Compass.cpp.o
[  8%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Display.cpp.o
[  8%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Gyroscope.cpp.o
[  9%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/I2C.cpp.o
[  9%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/SPI.cpp.o
[ 10%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Sensor.cpp.o
[ 10%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Serial.cpp.o
[ 10%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Timer.cpp.o
[ 11%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AnalogSensor.cpp.o
[ 11%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AnimatedDisplay.cpp.o
[ 11%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AsciiKeyMap.cpp.o
[ 12%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/Button.cpp.o
[ 12%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/FXOS8700.cpp.o
[ 12%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/GhostFAT.cpp.o
[ 13%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HID.cpp.o
[ 13%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDJoystick.cpp.o
[ 13%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDKeyboard.cpp.o
[ 14%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDMouse.cpp.o
[ 14%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ILI9341.cpp.o
[ 15%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/KeyValueStorage.cpp.o
[ 15%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LEDMatrix.cpp.o
[ 15%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LIS3DH.cpp.o
[ 16%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LSM303Accelerometer.cpp.o
[ 16%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LSM303Magnetometer.cpp.o
[ 16%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LinearAnalogSensor.cpp.o
[ 17%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MAG3110.cpp.o
[ 17%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MMA8653.cpp.o
[ 17%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MPU6050.cpp.o
[ 18%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MessageBus.cpp.o
[ 18%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MultiButton.cpp.o
[ 19%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/PearsonHash.cpp.o
[ 19%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/NonLinearAnalogSensor.cpp.o
[ 19%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/PulseIn.cpp.o
[ 20%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ST7735.cpp.o
[ 20%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ScreenIO.cpp.o
[ 20%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/StandardSPIFlash.cpp.o
[ 21%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/TouchButton.cpp.o
[ 21%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/TouchSensor.cpp.o
[ 21%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/USBMSC.cpp.o
[ 22%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/DataStream.cpp.o
[ 22%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/LevelDetector.cpp.o
[ 22%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/LevelDetectorSPL.cpp.o
[ 23%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/MemorySource.cpp.o
[ 23%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/Mixer.cpp.o
[ 24%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/StreamNormalizer.cpp.o
[ 24%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/Synthesizer.cpp.o
[ 24%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/BitmapFont.cpp.o
[ 25%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/CoordinateSystem.cpp.o
[ 25%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Event.cpp.o
[ 25%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Image.cpp.o
[ 26%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/ManagedBuffer.cpp.o
[ 26%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/ManagedString.cpp.o
[ 26%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Matrix4.cpp.o
[ 27%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/RefCounted.cpp.o
[ 27%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/RefCountedInit.cpp.o
[ 27%] Linking CXX static library ../../libcodal-core.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 27%] Built target codal-core
Scanning dependencies of target codal-rp2040
make[2]: Warning: File 'libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/depend.make' has modification time 1.5 s in the future
[ 28%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040I2C.cpp.o
[ 28%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040LowLevelTimer.cpp.o
[ 28%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040PWM.cpp.o
[ 29%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040Pin.cpp.o
[ 29%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040Spi.cpp.o
[ 29%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/RP2040USB.cpp.o
[ 30%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/ZSingleWireSerial.cpp.o
[ 30%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/codal_target_hal_base.cpp.o
[ 30%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/asm/CortexContextSwitch.s.o
[ 31%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/dma.c.o
/src/libraries/codal-rp2040/asm/CortexContextSwitch.s: Assembler messages:
/src/libraries/codal-rp2040/asm/CortexContextSwitch.s: Warning: end of file not at end of a line; newline inserted
[ 31%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/source/ram.c.o
[ 32%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/cmsis/stub/CMSIS/Device/RaspberryPi/RP2040/Source/system_RP2040.c.o
[ 32%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.o
[ 32%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_claim/claim.c.o
[ 33%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_platform/platform.c.o
[ 33%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_sync/sync.c.o
[ 33%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.o
[ 34%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_irq/irq.c.o
[ 34%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.o
[ 34%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_sync/sem.c.o
[ 35%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_sync/lock_core.c.o
[ 35%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_time/time.c.o
[ 35%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_time/timeout_helper.c.o
[ 36%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_timer/timer.c.o
[ 36%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_util/datetime.c.o
[ 37%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_util/pheap.c.o
[ 37%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_util/queue.c.o
[ 37%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_sync/mutex.c.o
[ 38%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/common/pico_sync/critical_section.c.o
[ 38%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_pll/pll.c.o
[ 38%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.o
[ 39%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.o
[ 39%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.o
[ 39%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_spi/spi.c.o
[ 40%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_i2c/i2c.c.o
[ 40%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_uart/uart.c.o
[ 41%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_flash/flash.c.o
[ 41%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.o
[ 41%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_pio/pio.c.o
[ 42%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_dma/dma.c.o
[ 42%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_exception/exception.c.o
[ 42%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/hardware_divider/divider.S.o
[ 43%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_runtime/runtime.c.o
[ 43%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_printf/printf.c.o
[ 43%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.o
[ 44%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_divider/divider.S.o
[ 44%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.o
[ 44%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.o
[ 45%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_double/double_math.c.o
[ 45%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.o
[ 46%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.o
[ 46%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.o
[ 46%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.o
[ 47%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_float/float_math.c.o
[ 47%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.o
[ 47%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.o
[ 48%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.o
[ 48%] Building ASM object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.o
[ 48%] Building CXX object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.o
[ 49%] Building C object libraries/codal-rp2040/CMakeFiles/codal-rp2040.dir/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.o
[ 49%] Linking CXX static library ../../libcodal-rp2040.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 49%] Built target codal-rp2040
Scanning dependencies of target codal-pi-pico
make[2]: Warning: File 'libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/depend.make' has modification time 1.5 s in the future
[ 50%] Building CXX object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/model/PiPico.cpp.o
[ 50%] Building CXX object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/model/PiPicoIO.cpp.o
[ 51%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/cmsis/stub/CMSIS/Device/RaspberryPi/RP2040/Source/system_RP2040.c.o
[ 51%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.o
[ 51%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_claim/claim.c.o
[ 52%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_platform/platform.c.o
[ 52%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_sync/sync.c.o
[ 52%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.o
[ 53%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_irq/irq.c.o
[ 53%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.o
[ 53%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_sync/sem.c.o
[ 54%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_sync/lock_core.c.o
[ 54%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_time/time.c.o
[ 55%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_time/timeout_helper.c.o
[ 55%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_timer/timer.c.o
[ 55%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_util/datetime.c.o
[ 56%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_util/pheap.c.o
[ 56%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_util/queue.c.o
[ 56%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_sync/mutex.c.o
[ 57%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/common/pico_sync/critical_section.c.o
[ 57%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_pll/pll.c.o
[ 57%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.o
[ 58%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.o
[ 58%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.o
[ 58%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_spi/spi.c.o
[ 59%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_i2c/i2c.c.o
[ 59%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_uart/uart.c.o
[ 60%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_flash/flash.c.o
[ 60%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.o
[ 60%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_pio/pio.c.o
[ 61%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_dma/dma.c.o
[ 61%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_exception/exception.c.o
[ 61%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/hardware_divider/divider.S.o
[ 62%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_runtime/runtime.c.o
[ 62%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_printf/printf.c.o
[ 62%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.o
[ 63%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_divider/divider.S.o
[ 63%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.o
[ 64%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.o
[ 64%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_math.c.o
[ 64%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.o
[ 65%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.o
[ 65%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.o
[ 65%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.o
[ 66%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_math.c.o
[ 66%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.o
[ 66%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.o
[ 67%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.o
[ 67%] Building ASM object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.o
[ 67%] Building CXX object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.o
[ 68%] Building C object libraries/codal-pi-pico/CMakeFiles/codal-pi-pico.dir/__/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.o
[ 68%] Linking CXX static library ../../libcodal-pi-pico.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 68%] Built target codal-pi-pico
Scanning dependencies of target PI-PICO
make[2]: Warning: File 'CMakeFiles/PI-PICO.dir/depend.make' has modification time 1.5 s in the future
[ 68%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/accelerometer/accelerometer.cpp.o
[ 68%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/accelerometer/accelhw.cpp.o
[ 69%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/advmath.cpp.o
[ 69%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/buffer.cpp.o
[ 69%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/control.cpp.o
[ 70%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/controlgc.cpp.o
[ 70%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/core.cpp.o
[ 70%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/gc.cpp.o
[ 71%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/loops.cpp.o
[ 71%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/pxt.cpp.o
[ 71%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/base/trig.cpp.o
[ 72%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/buttons/buttons.cpp.o
[ 72%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/codal.cpp.o
[ 73%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/control.cpp.o
[ 73%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/dmac.cpp.o
[ 73%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/hf2.cpp.o
[ 74%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/i2c.cpp.o
[ 74%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/keyvaluestorage.cpp.o
[ 74%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/light.cpp.o
[ 75%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/pins.cpp.o
[ 75%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/pinsAnalog.cpp.o
[ 75%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/pinsDigital.cpp.o
[ 76%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/pinsPWM.cpp.o
[ 76%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/platform.cpp.o
[ 76%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/spi.cpp.o
[ 77%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/core---rp2040/usb.cpp.o
[ 77%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/lcd/lcd.cpp.o
[ 78%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/lightsensor/lightsensor.cpp.o
[ 78%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/main.cpp.o
[ 78%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/mixer---rp2040/melody.cpp.o
[ 79%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/mixer---rp2040/sound.cpp.o
[ 79%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/pointers.cpp.o
[ 79%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/screen---st7735/image.cpp.o
[ 80%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/screen---st7735/jddisplay.cpp.o
[ 80%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/screen---st7735/panic.cpp.o
[ 80%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/screen---st7735/screen.cpp.o
[ 81%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/switch/switch.cpp.o
[ 81%] Building CXX object CMakeFiles/PI-PICO.dir/pxtapp/thermometer/temperature.cpp.o
[ 82%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/cmsis/stub/CMSIS/Device/RaspberryPi/RP2040/Source/system_RP2040.c.o
[ 82%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_clocks/clocks.c.o
[ 82%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_claim/claim.c.o
[ 83%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_platform/platform.c.o
[ 83%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_sync/sync.c.o
[ 83%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_gpio/gpio.c.o
[ 84%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_irq/irq.c.o
[ 84%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_irq/irq_handler_chain.S.o
[ 84%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_sync/sem.c.o
[ 85%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_sync/lock_core.c.o
[ 85%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_time/time.c.o
[ 85%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_time/timeout_helper.c.o
[ 86%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_timer/timer.c.o
[ 86%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_util/datetime.c.o
[ 87%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_util/pheap.c.o
[ 87%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_util/queue.c.o
[ 87%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_sync/mutex.c.o
[ 88%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/common/pico_sync/critical_section.c.o
[ 88%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_pll/pll.c.o
[ 88%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_vreg/vreg.c.o
[ 89%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_watchdog/watchdog.c.o
[ 89%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_xosc/xosc.c.o
[ 89%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_spi/spi.c.o
[ 90%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_i2c/i2c.c.o
[ 90%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_uart/uart.c.o
[ 91%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_flash/flash.c.o
[ 91%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_bootrom/bootrom.c.o
[ 91%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_pio/pio.c.o
[ 92%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_dma/dma.c.o
[ 92%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_exception/exception.c.o
[ 92%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/hardware_divider/divider.S.o
[ 93%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_runtime/runtime.c.o
[ 93%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_printf/printf.c.o
[ 93%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_bit_ops/bit_ops_aeabi.S.o
[ 94%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_divider/divider.S.o
[ 94%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_aeabi.S.o
[ 94%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_init_rom.c.o
[ 95%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_math.c.o
[ 95%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_double/double_v1_rom_shim.S.o
[ 96%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_int64_ops/pico_int64_ops_aeabi.S.o
[ 96%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_aeabi.S.o
[ 96%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_init_rom.c.o
[ 97%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_math.c.o
[ 97%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_float/float_v1_rom_shim.S.o
[ 97%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_malloc/pico_malloc.c.o
[ 98%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_mem_ops/mem_ops_aeabi.S.o
[ 98%] Building ASM object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/crt0.S.o
[ 98%] Building CXX object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/new_delete.cpp.o
[ 99%] Building C object CMakeFiles/PI-PICO.dir/libraries/codal-rp2040/pico-sdk/src/rp2_common/pico_standard_link/binary_info.c.o
[ 99%] Linking CXX executable PI-PICO
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 99%] Built target PI-PICO
Scanning dependencies of target PI-PICO_hex
Scanning dependencies of target PI-PICO_bin
make[2]: Warning: File 'PI-PICO' has modification time 1.4 s in the future
make[2]: Warning: File 'PI-PICO' has modification time 1.4 s in the future
[100%] converting to hex file.
[100%] converting to bin file.
Executing post process command
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[100%] Built target PI-PICO_hex
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[100%] Built target PI-PICO_bin
make[1]: warning:  Clock skew detected.  Your build may be incomplete.
building bundled libs/settings
building bundled libs/settings---files
building bundled libs\blocksprj
[run] git clone https://github.com/lancaster-university/codal built/dockercodal
Cloning into 'built/dockercodal'...
remote: Enumerating objects: 2999, done.
remote: Counting objects: 100% (94/94), done.
remote: Compressing objects: 100% (46/46), done.
remote: Total 2999 (delta 51), reused 81 (delta 48), pack-reused 2905
Receiving objects: 100% (2999/2999), 1.38 MiB | 6.03 MiB/s, done.
Resolving deltas: 100% (1966/1966), done.
[run] cd built/dockercodal; git checkout v0.9.0
Note: switching to 'v0.9.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; git checkout v0.9.0
HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; git checkout v0.9.0
HEAD is now at e1bb097 Merge pull request #44 from lancaster-university/rp2040-build
[run] cd built/dockercodal; docker run --rm -v D:\makecode\pxt_pico\libs\blocksprj/built/dockercodal/:/src -w /src -u build pext/yotta:latest python build.py
Creating libraries folder
Cloning into: https://github.com/lancaster-university/codal-circuit-playground
Cloning into 'codal-circuit-playground'...
Checking out branch: v2.0.4
HEAD is now at 38e9bf4... Snapshot v2.0.4
Set target: codal-circuit-playground
Using target-locked.json
Targeting codal-circuit-playground
-- The C compiler identification is GNU 6.2.1
-- The CXX compiler identification is GNU 6.2.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- The ASM compiler identification is GNU
-- Found assembler: /usr/bin/arm-none-eabi-gcc
Installing dependencies...
-- Adding library path: (/src/libraries)
Cloning into: https://github.com/lancaster-university/codal-core
Cloning into 'codal-core'...
Checking out branch: 312ae57e0b31f5b9df07a81e9d846945828e3c5a
HEAD is now at 312ae57... PR feedback
Cloning into: https://github.com/lancaster-university/codal-samd
Cloning into 'codal-samd'...
Submodule 'asf4' (https://github.com/lancaster-university/asf4) registered for path 'asf4'
Submodule 'samd-peripherals' (https://github.com/lancaster-university/samd-peripherals) registered for path 'samd-peripherals'
Cloning into 'asf4'...
Submodule path 'asf4': checked out '6664673f70d9170b4374a726c5322e9be6b3f237'
Cloning into 'samd-peripherals'...
Submodule path 'samd-peripherals': checked out '96563308fc7b97646cbe429953e79cb3405846f0'
Checking out branch: 5bd6b93c219c7e784e885ba2d6812809fb6289a8
HEAD is now at 5bd6b93... Disable logging
Synchronizing submodule url for 'asf4'
Synchronizing submodule url for 'samd-peripherals'
Using library: codal-circuit-playground
Using library: codal-core
Using library: codal-samd
-- Configuring done
-- Generating done
-- Build files have been written to: /src/build
make: Warning: File `Makefile' has modification time 0.87 s in the future
make[1]: Warning: File `CMakeFiles/Makefile2' has modification time 1.5 s in the future
make[2]: Warning: File `libraries/codal-core/CMakeFiles/codal-core.dir/flags.make' has modification time 1.1 s in the future
Scanning dependencies of target codal-core
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
make[2]: Warning: File `libraries/codal-core/CMakeFiles/codal-core.dir/depend.make' has modification time 1.3 s in the future
[  0%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/JACDAC.cpp.o
[  1%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/JDPhysicalLayer.cpp.o
[  1%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/JDService.cpp.o
[  2%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDCRC.cpp.o
[  2%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDConfigurationService.cpp.o
[  3%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDControlService.cpp.o
[  3%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDDeviceManager.cpp.o
[  4%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDGPIOIdentification.cpp.o
[  4%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDRNGService.cpp.o
[  5%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/control/JDSoundIdentification.cpp.o
[  6%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/services/JDAccelerometerService.cpp.o
[  6%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/services/JDConsoleService.cpp.o
[  7%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/services/JDMessageBusService.cpp.o
[  7%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/services/JDPacketSniffer.cpp.o
[  8%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/JACDAC/services/JDTestService.cpp.o
[  8%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalCompat.cpp.o
[  9%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalComponent.cpp.o
/src/libraries/codal-core/source/JACDAC/control/JDSoundIdentification.cpp: In member function 'void codal::JDSoundIdentification::identify(codal::Event)':
/src/libraries/codal-core/source/JACDAC/control/JDSoundIdentification.cpp:24:9: warning: unused variable 'state' [-Wunused-variable]
     int state = 0;
         ^~~~~
[  9%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalDevice.cpp.o
[ 10%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalDmesg.cpp.o
[ 10%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalFiber.cpp.o
[ 11%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalHeapAllocator.cpp.o
[ 11%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalListener.cpp.o
/src/libraries/codal-core/source/JACDAC/services/JDTestService.cpp: In member function 'virtual int codal::JDTestService::handlePacket(codal::JDPacket*)':
/src/libraries/codal-core/source/JACDAC/services/JDTestService.cpp:12:70: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
     DMESG("REC N: %d F: %d->%d N: %s M: %c%c%c", *((uint32_t*)p->data), p->device_address, p->service_number, this->name.toCharArray(), (this->mode == ClientService) ? "C":"", (this->mode == HostService) ? "H":"", (this->mode == BroadcastHostService) ? "B":"");
                                                                      ^
[ 12%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/CodalUtil.cpp.o
[ 13%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/MemberFunctionCallback.cpp.o
[ 13%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/core/codal_default_target_hal.cpp.o
[ 14%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/AbstractButton.cpp.o
[ 14%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Accelerometer.cpp.o
[ 15%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/CodalUSB.cpp.o
[ 15%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Compass.cpp.o
[ 16%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Display.cpp.o
[ 16%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Gyroscope.cpp.o
[ 17%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/I2C.cpp.o
[ 17%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/SPI.cpp.o
[ 18%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Sensor.cpp.o
[ 18%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Serial.cpp.o
[ 19%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/driver-models/Timer.cpp.o
[ 19%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AnalogSensor.cpp.o
[ 20%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AnimatedDisplay.cpp.o
[ 21%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/AsciiKeyMap.cpp.o
[ 21%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/Button.cpp.o
[ 22%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/FXOS8700Accelerometer.cpp.o
[ 22%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/FXOS8700.cpp.o
/src/libraries/codal-core/source/driver-models/Serial.cpp:862:6: warning: #warning define API for pin swap... [-Wcpp]
     #warning define API for pin swap...
      ^~~~~~~
[ 23%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/FXOS8700Magnetometer.cpp.o
[ 23%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/GhostFAT.cpp.o
/tmp/ccpxs2q1.s: Assembler messages:
/tmp/ccpxs2q1.s:116: Warning: ignoring changed section attributes for .data
[ 24%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HID.cpp.o
[ 24%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDJoystick.cpp.o
[ 25%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDKeyboard.cpp.o
[ 25%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/HIDMouse.cpp.o
[ 26%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ILI9341.cpp.o
[ 26%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/KeyValueStorage.cpp.o
[ 27%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LEDMatrix.cpp.o
[ 27%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LIS3DH.cpp.o
[ 28%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/LinearAnalogSensor.cpp.o
[ 29%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MAG3110.cpp.o
[ 29%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MMA8653.cpp.o
[ 30%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MPU6050.cpp.o
[ 30%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MessageBus.cpp.o
[ 31%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/MultiButton.cpp.o
[ 31%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/NonLinearAnalogSensor.cpp.o
[ 32%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/PearsonHash.cpp.o
[ 32%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ST7735.cpp.o
[ 33%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/ScreenIO.cpp.o
[ 33%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/StandardSPIFlash.cpp.o
[ 34%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/TouchButton.cpp.o
[ 34%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/TouchSensor.cpp.o
[ 35%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/USBJACDAC.cpp.o
[ 35%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/drivers/USBMSC.cpp.o
[ 36%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/DataStream.cpp.o
[ 37%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/LevelDetector.cpp.o
[ 37%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/LevelDetectorSPL.cpp.o
[ 38%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/Mixer.cpp.o
[ 38%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/StreamNormalizer.cpp.o
[ 39%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/streams/Synthesizer.cpp.o
[ 39%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/BitmapFont.cpp.o
[ 40%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/CoordinateSystem.cpp.o
[ 40%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Event.cpp.o
[ 41%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Image.cpp.o
[ 41%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/ManagedBuffer.cpp.o
[ 42%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/ManagedString.cpp.o
[ 42%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/Matrix4.cpp.o
[ 44%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/RefCounted.cpp.o
[ 44%] Building CXX object libraries/codal-core/CMakeFiles/codal-core.dir/source/types/RefCountedInit.cpp.o
[ 44%] Linking CXX static library ../../libcodal-core.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 44%] Built target codal-core
Scanning dependencies of target codal-samd
make[2]: Warning: File `libraries/codal-samd/CMakeFiles/codal-samd.dir/depend.make' has modification time 0.94 s in the future
[ 45%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/clocks.c.o
[ 45%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/clocks.c.o
[ 46%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/external_interrupts.c.o
[ 46%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/external_interrupts.c.o
[ 47%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/cache.c.o
[ 47%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/i2s.c.o
[ 48%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/i2s.c.o
[ 48%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/timers.c.o
[ 49%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/pins.c.o
[ 49%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/pins.c.o
[ 50%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/timers.c.o
[ 50%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/sercom.c.o
[ 51%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/sercom.c.o
[ 52%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/samd-peripherals/samd/samd21/adc.c.o
[ 52%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_atomic.c.o
[ 53%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_spi_m_sync.c.o
[ 53%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_usart_async.c.o
[ 54%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_adc_sync.c.o
[ 54%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_i2c_m_sync.c.o
[ 55%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hal/src/hal_io.c.o
[ 55%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hpl/sercom/hpl_sercom.c.o
[ 56%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/asf4/samd21/hpl/adc/hpl_adc.c.o
[ 56%] Building ASM object libraries/codal-samd/CMakeFiles/codal-samd.dir/asm/CortexContextSwitch.s.o
[ 57%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/CapTouchButton.cpp.o
[ 57%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/DmaFactory.cpp.o
[ 58%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/DmaInstance.cpp.o
[ 58%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDDAC.cpp.o
[ 59%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDEIC.cpp.o
[ 60%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDNVM.cpp.o
[ 60%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDPDM.cpp.o
[ 61%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDSerial.cpp.o
[ 61%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDTCCTimer.cpp.o
/src/libraries/codal-samd/asf4/samd21/hpl/sercom/hpl_sercom.c: In function '_spi_m_dma_set_char_size':
/src/libraries/codal-samd/asf4/samd21/hpl/sercom/hpl_sercom.c:3341:10: warning: 'size' may be used uninitialized in this function [-Wmaybe-uninitialized]
  uint8_t size;
          ^~~~
[ 62%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDTCTimer.cpp.o
[ 62%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/SAMDUSB.cpp.o
[ 63%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/ZI2C.cpp.o
[ 63%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/ZPin.cpp.o
[ 64%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/ZSPI.cpp.o
[ 64%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/ZSingleWireSerial.cpp.o
[ 65%] Building CXX object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/adafruit_ptc.cpp.o
[ 65%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/pinmap.c.o
[ 66%] Building C object libraries/codal-samd/CMakeFiles/codal-samd.dir/src/pwmout.c.o
/src/libraries/codal-samd/src/ZI2C.cpp: In member function 'void codal::ZI2C::reset()':
/src/libraries/codal-samd/src/ZI2C.cpp:45:9: warning: variable 'ret' set but not used [-Wunused-but-set-variable]
     int ret = 0;
         ^~~
[ 67%] Linking CXX static library ../../libcodal-samd.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 67%] Built target codal-samd
Scanning dependencies of target codal-circuit-playground
make[2]: Warning: File `libraries/codal-circuit-playground/CMakeFiles/codal-circuit-playground.dir/depend.make' has modification time 1.1 s in the future
[ 68%] Building CXX object libraries/codal-circuit-playground/CMakeFiles/codal-circuit-playground.dir/source/codal_target_hal.cpp.o
[ 68%] Building CXX object libraries/codal-circuit-playground/CMakeFiles/codal-circuit-playground.dir/model/CircuitPlayground.cpp.o
[ 69%] Building CXX object libraries/codal-circuit-playground/CMakeFiles/codal-circuit-playground.dir/model/CircuitPlaygroundIO.cpp.o
[ 69%] Building C object libraries/codal-circuit-playground/CMakeFiles/codal-circuit-playground.dir/source/startup_samd21.c.o
[ 70%] Linking CXX static library ../../libcodal-circuit-playground.a
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 70%] Built target codal-circuit-playground
Scanning dependencies of target CIRCUIT_PLAYGROUND
make[2]: Warning: File `CMakeFiles/CIRCUIT_PLAYGROUND.dir/depend.make' has modification time 0.9 s in the future
[ 70%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/accelerometer/accelerometer.cpp.o
[ 71%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/accelerometer/accelhw.cpp.o
[ 71%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/advmath.cpp.o
[ 72%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/buffer.cpp.o
[ 72%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/control.cpp.o
[ 73%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/controlgc.cpp.o
[ 73%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/core.cpp.o
[ 74%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/gc.cpp.o
[ 74%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/loops.cpp.o
[ 75%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/pxt.cpp.o
/src/pxtapp/base/core.cpp: In function 'void pxt::setupSkipList(pxt::String, const char*, int)':
/src/pxtapp/base/core.cpp:212:36: warning: unknown option after '#pragma GCC diagnostic' kind [-Wpragmas]
     #pragma GCC diagnostic ignored "-Wstringop-overflow"
                                    ^~~~~~~~~~~~~~~~~~~~~
[ 75%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/base/trig.cpp.o
[ 76%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/buttons/buttons.cpp.o
[ 76%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/codal.cpp.o
[ 77%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/control.cpp.o
[ 78%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/dmac.cpp.o
[ 78%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/hf2.cpp.o
[ 79%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/i2c.cpp.o
[ 79%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/keyvaluestorage.cpp.o
[ 80%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/light.cpp.o
[ 80%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/pins.cpp.o
[ 81%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/pinsAnalog.cpp.o
[ 81%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/pinsDigital.cpp.o
[ 82%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/pinsPWM.cpp.o
[ 82%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/platform.cpp.o
[ 83%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/spi.cpp.o
[ 83%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/core---samd/usb.cpp.o
[ 84%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/game/controllerbuttons.cpp.o
[ 84%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/game/targetoverrides.cpp.o
[ 85%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/lcd/lcd.cpp.o
[ 86%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/lightsensor/lightsensor.cpp.o
[ 86%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/main.cpp.o
[ 87%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/microphone/microphone.cpp.o
[ 87%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/microphone/microphonehw.cpp.o
[ 88%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/mixer---samd/melody.cpp.o
[ 88%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/mixer---samd/sound.cpp.o
[ 89%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/pointers.cpp.o
[ 89%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/screen---st7735/image.cpp.o
[ 90%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/screen---st7735/jddisplay.cpp.o
[ 90%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/screen---st7735/panic.cpp.o
[ 91%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/screen---st7735/screen.cpp.o
[ 91%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/serial/serial-common.cpp.o
[ 92%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/serial/serial-target.cpp.o
[ 92%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/NRF52Flash.cpp.o
[ 93%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/RAFFS.cpp.o
[ 94%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/RP2040Flash.cpp.o
In file included from /src/pxtapp/pointers.cpp:26:0:
/src/pxtapp/storage/SNORFS.h:6:0: warning: "DEVICE_FLASH_ERROR" redefined
 #define DEVICE_FLASH_ERROR 950

In file included from /src/pxtapp/settings/RAFFS.h:4:0,
                 from /src/pxtapp/pointers.cpp:24:
/src/pxtapp/settings/Flash.h:39:0: note: this is the location of the previous definition
 #define DEVICE_FLASH_ERROR 922

/src/pxtapp/screen---st7735/jddisplay.cpp: In member function 'void pxt::JDDisplay::handleIncoming(jd_packet_t*)':
/src/pxtapp/screen---st7735/jddisplay.cpp:160:52: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
             soundBufferPending = *(uint32_t *)pkt->data;
                                                    ^~~~
/src/pxtapp/screen---st7735/jddisplay.cpp:163:49: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
             soundSampleRate = *(uint32_t *)pkt->data >> 10;
                                                 ^~~~
/src/pxtapp/screen---st7735/jddisplay.cpp:169:46: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
             screenHeight = *(uint16_t *)pkt->data;
                                              ^~~~
/src/pxtapp/screen---st7735/jddisplay.cpp:172:45: warning: dereferencing type-punned pointer will break strict-aliasing rules [-Wstrict-aliasing]
             screenWidth = *(uint16_t *)pkt->data;
                                             ^~~~
[ 94%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/SAMDFlash.cpp.o
[ 95%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/STM32Flash.cpp.o
[ 95%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/settings/settings.cpp.o
[ 96%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/storage/GhostSNORFS.cpp.o
[ 96%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/storage/SNORFS.cpp.o
[ 97%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/storage/storage.cpp.o
[ 97%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/switch/switch.cpp.o
[ 98%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/thermometer/temperature.cpp.o
[ 98%] Building CXX object CMakeFiles/CIRCUIT_PLAYGROUND.dir/pxtapp/touch/touch.cpp.o
[ 99%] Linking CXX executable CIRCUIT_PLAYGROUND
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[ 99%] Built target CIRCUIT_PLAYGROUND
Scanning dependencies of target CIRCUIT_PLAYGROUND_bin
Scanning dependencies of target CIRCUIT_PLAYGROUND_hex
make[2]: Warning: File `CIRCUIT_PLAYGROUND' has modification time 1.4 s in the future
make[2]: Warning: File `CIRCUIT_PLAYGROUND' has modification time 1.4 s in the future
[100%] converting to bin file.
[100%] converting to hex file.
Executing post process command
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[100%] Built target CIRCUIT_PLAYGROUND_hex
Converting to uf2, output size: 332800, start address: 0x2000
Wrote 332800 bytes to /src/build/CIRCUIT_PLAYGROUND.uf2
make[2]: warning:  Clock skew detected.  Your build may be incomplete.
[100%] Built target CIRCUIT_PLAYGROUND_bin
make[1]: warning:  Clock skew detected.  Your build may be incomplete.
make: warning:  Clock skew detected.  Your build may be incomplete.
target-strings.json built
target.json built.
building sim...
[run] cd sim; node ../node_modules/typescript/bin/tsc
[run] node D:\makecode\pxt_pico\node_modules\pxt-core\node_modules\less\bin\lessc theme/style.less built/web/semantic.css --include-path=node_modules/semantic-ui-less:node_modules/pxt-core/theme:theme/foo/bar:theme:node_modules/pxt-core/react-common/styles:react-common/styles:node_modules/@fortawesome:node_modules/pxt-core/node_modules/@fortawesome
[run] node D:\makecode\pxt_pico\node_modules\pxt-core\node_modules\less\bin\lessc theme/blockly.less built/web/blockly.css --include-path=node_modules/semantic-ui-less:node_modules/pxt-core/theme:theme/foo/bar:theme:node_modules/pxt-core/react-common/styles:react-common/styles:node_modules/@fortawesome:node_modules/pxt-core/node_modules/@fortawesome
[run] node D:\makecode\pxt_pico\node_modules\pxt-core\node_modules\less\bin\lessc node_modules/pxt-core/react-common/styles/react-common-skillmap.less built/web/react-common-skillmap.css --include-path=node_modules/semantic-ui-less:node_modules/pxt-core/theme:theme/foo/bar:theme:node_modules/pxt-core/react-common/styles:react-common/styles:node_modules/@fortawesome:node_modules/pxt-core/node_modules/@fortawesome

D:\makecode\pxt_pico>


// codal.json file contents:

{
    "target": {
        "name": "codal-pi-pico",
        "url": "https://github.com/lancaster-university/codal-pi-pico",
        "branch": "v0.0.10",
        "type": "git"
    },
    "definitions": {
        "PXT_SUPPORT_LIS3DH": 1,
        "PXT_SUPPORT_MMA8653": 1,
        "PXT_SUPPORT_MMA8453": 1,
        "PXT_SUPPORT_FXOS8700": 0,
        "PXT_SUPPORT_MPU6050": 1,
        "PXT_GC_CHECKS": 0,
        "PXT_BOARD_ID": "BOARD_ID_CPLAY",
        "DEVICE_COMPONENT_COUNT": 64,
        "DEVICE_DMESG_BUFFER_SIZE": 1024,
        "PXT_TARGET": "\"maker\""
    },
    "config": {
        "PXT_SUPPORT_LIS3DH": 1,
        "PXT_SUPPORT_MMA8653": 1,
        "PXT_SUPPORT_MMA8453": 1,
        "PXT_SUPPORT_FXOS8700": 0,
        "PXT_SUPPORT_MPU6050": 1,
        "PXT_GC_CHECKS": 0,
        "PXT_BOARD_ID": "BOARD_ID_CPLAY",
        "DEVICE_COMPONENT_COUNT": 64,
        "DEVICE_DMESG_BUFFER_SIZE": 1024,
        "PXT_TARGET": "\"maker\""
    },
    "application": "pxtapp",
    "output_folder": "build",
    "pxt_gitrepo": "lancaster-university/codal",
    "pxt_gittag": "v0.9.0"
}

//

```