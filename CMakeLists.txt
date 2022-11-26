cmake_minimum_required(VERSION 3.13)

# initialize pico-sdk from submodule
# note: this must happen before project()
include(pico-sdk/pico_sdk_init.cmake)

project(lvgl_rp2040_sh1107)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# lvgl
include_directories(
    . # for lv_conf.h
)
add_subdirectory(lvgl)

# eez-framework
include_directories(
    eez-framework/src
)
add_definitions(-DEEZ_FOR_LVGL -DEEZ_PLATFORM_PICO)
file(GLOB_RECURSE EEZ_FRAMEWORK_SOURCES
    eez-framework/src/eez/*.cpp
    eez-framework/src/eez/*.c
)
# /eez-framework

# my sources
file(GLOB MY_SOURCES
   main.c
   ui/*.c
)

set(ALL_SOURCES)
list(APPEND ALL_SOURCES ${EEZ_FRAMEWORK_SOURCES})
list(APPEND ALL_SOURCES ${MY_SOURCES})

add_executable(
    lvgl_rp2040_sh1107
    ${ALL_SOURCES}
)

target_link_libraries(lvgl_rp2040_sh1107 pico_stdlib hardware_i2c lvgl)

pico_add_extra_outputs(lvgl_rp2040_sh1107)

pico_enable_stdio_usb(lvgl_rp2040_sh1107 1)
pico_enable_stdio_uart(lvgl_rp2040_sh1107 0)
