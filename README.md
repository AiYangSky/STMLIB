# STMLIBs
This repository is used to host STM32 library files and build them into corresponding library files using GUN.

# Note:
	Startup and link files are not provided.
	
# How to use:
	Add "add_subdirectory(${DIR}/STMLIB)" to the parent directory and use "target_link_libraries(<project> stm32lib) "to linking.
	Use STM32_CHIP_TYPE to specify the chip type and STM32_LIB_TYPE to specify the library type.
	Default HSE = 8 MHz; HSI = 16 MHZ; The interrupt vector is offset by 0X00.
	The files "system_stm32fxxx.c" and "stm32fxxx.h" can be overwritten to adjust the system configuration by defining STM32_LIB_SYSTEM_FILE and STM32_LIB_HEAD_FILE, respectively.
 
# Support list:
	STM32F4,std_lib				STM32_CHIP_TYPE = stm32f4	STM32_LIB_TYPE = std
	
	

	
