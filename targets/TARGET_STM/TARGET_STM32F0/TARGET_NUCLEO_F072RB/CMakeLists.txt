# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(STARTUP_FILE device/TOOLCHAIN_GCC_ARM/startup_stm32f072xb.S)
    set(LINKER_FILE device/TOOLCHAIN_GCC_ARM/STM32F072XB.ld)
elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(STARTUP_FILE device/TOOLCHAIN_ARM/startup_stm32f072xb.S)
    set(LINKER_FILE device/TOOLCHAIN_ARM/stm32f072xb.sct)
endif()

set_property(GLOBAL PROPERTY MBED_TARGET_LINKER_FILE ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_sources(mbed-core
    INTERFACE
        PeripheralPins.c
        device/system_clock.c
        device/cmsis_nvic.c
        ${STARTUP_FILE}
)

target_include_directories(mbed-core
    INTERFACE
        .
        device
)
