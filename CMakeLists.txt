cmake_minimum_required(VERSION 3.13)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(pico_sdk_import.cmake)

project(semtech-pico-hal C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

file(GLOB_RECURSE SYSTEM RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "src/system/*.[ch]")
file(GLOB_RECURSE BOARDS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "src/boards/*.[ch]")

pico_sdk_init()

add_library( semtech-pico-hal
    ${SYSTEM}
    ${BOARDS}
)

target_link_libraries(semtech-pico-hal
    pico_stdlib
    pico_multicore
    hardware_irq
    pico_unique_id
    hardware_flash
    hardware_spi
)

target_include_directories(semtech-pico-hal
    PUBLIC
    include
    semtech-pico-hal/include
    "${CMAKE_CURRENT_SOURCE_DIR}"
)

