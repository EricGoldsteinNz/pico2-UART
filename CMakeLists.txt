# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.0)
set(toolchainVersion 13_3_Rel1)
set(picotoolVersion 2.1.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
# Set the target build to pico2 so that its built for RP2350 instead of RP2040
set(PICO_BOARD pico2)
cmake_minimum_required(VERSION 3.13)
include(pico_sdk_import.cmake)

project(pico_uart_bridge)

pico_sdk_init()

add_executable(pico2-UART uart-bridge.c usb-descriptors.c)

target_include_directories(pico2-UART PUBLIC
	${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(pico2-UART
	hardware_flash
	pico_multicore
	pico_unique_id
	pico_stdlib
	tinyusb_device
	tinyusb_board)

pico_add_extra_outputs(pico2-UART)
