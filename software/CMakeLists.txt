cmake_minimum_required(VERSION 3.13)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(gbpunk)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# rest of your project
add_executable(main)

# by default the header is generated into the build dir
pico_generate_pio_header(main ${CMAKE_CURRENT_LIST_DIR}/gbbus.pio)
# however, alternatively you can choose to generate it somewhere else (in this case in the source tree for check in)
#pico_generate_pio_header(main ${CMAKE_CURRENT_LIST_DIR}/blink.pio OUTPUT_DIR ${CMAKE_CURRENT_LIST_DIR})

target_sources(main PRIVATE main.c)

target_link_libraries(main PRIVATE pico_stdlib hardware_pio)
pico_enable_stdio_usb(main 1)
pico_add_extra_outputs(main)