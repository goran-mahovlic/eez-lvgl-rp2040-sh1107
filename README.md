# RP2040 toolchain with EEZ framework

## Prerequisites

```
sudo apt install gcc-arm-none-eabi
```

## Get sources and build

```
git clone --recurse-submodules https://github.com/goran-mahovlic/eez-lvgl-rp2040-sh1107.git
cd eez-lvgl-rp2040-sh1107
mkdir build
cd build
cmake ../
make
```
