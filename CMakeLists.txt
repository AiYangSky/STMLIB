set(PATH_STM32_LIB "${CMAKE_CURRENT_SOURCE_DIR}/${CHIP_TYPE}/${CHIP_LIB_TYPE}")

file(GLOB SRC_STM32_LIB ${PATH_STM32_LIB}/src/*.c)

if(NOT STM32_LIB_SYSTEM_FILE)
    file(GLOB STM32_LIB_SYSTEM_FILE ${CMAKE_CURRENT_LIST_DIR}/${CHIP_TYPE}/system/*.c)
    message(STATUS "Using default system_stm32fxxx.c file")
else()
    message(STATUS "Using custom system_stm32fxxx.c file by ${STM32_LIB_SYSTEM_FILE}")
endif()


set(CUSTOM_INC_DIR ${CMAKE_CURRENT_BINARY_DIR}/custom_inc)
if(NOT STM32_LIB_HEAD_FILE)
    file(GLOB STM32_LIB_HEAD_FILE ${CMAKE_CURRENT_LIST_DIR}/${CHIP_TYPE}/${CHIP_LIB_TYPE}/*.h)
    message(STATUS "Using default stm32fxxx.h file")
else()
    message(STATUS "Using custom stm32fxxx.h file by ${STM32_LIB_HEAD_FILE}")
endif()
STRING(REGEX REPLACE ".+/(.+)\\..*" "\\1" STM32_LIB_HEAD_FILE_NAME ${STM32_LIB_HEAD_FILE})
configure_file(${STM32_LIB_HEAD_FILE} ${CUSTOM_INC_DIR}/${STM32_LIB_HEAD_FILE_NAME}.h COPYONLY)

add_library(stm32lib)

target_sources(stm32lib
    PRIVATE
    ${SRC_STM32_LIB}
    ${STM32_LIB_SYSTEM_FILE}
)

target_include_directories(stm32lib
    PUBLIC
    ${PATH_STM32_LIB}/inc
    ${CMAKE_CURRENT_LIST_DIR}/${CHIP_TYPE}/system 
    ${CMAKE_CURRENT_LIST_DIR}/arm_cmsis
    ${CMAKE_CURRENT_BINARY_DIR}/custom_inc
)