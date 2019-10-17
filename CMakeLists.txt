cmake_minimum_required(VERSION 3.5)

if (${EVERGATEWAY_BUILD})
else()
    set(USB_INCLUDE "/usr/include/libusb-1.0")
    set(USB_LIB "/lib/x86_64-linux-gnu")
endif()

project(dfu-util)

add_definitions(-DHAVE_CONFIG_H)

set(DFU_FILES
    src/main.c
    src/dfu_load.c
    src/dfu_util.c
    src/dfuse.c
    src/dfuse_mem.c
    src/dfu.c
    src/dfu_file.c 
    src/quirks.c 
)

include_directories(
    .
    src
    "${USB_INCLUDE}"
)

link_directories(
        "${USB_LIB}"
)

add_executable(dfu-util ${DFU_FILES})

target_link_libraries(dfu-util
    usb-1.0
)

install(TARGETS dfu-util DESTINATION usr/bin/everactive )


