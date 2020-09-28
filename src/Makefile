#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# Makefile for the cortex-m4 and HOST build systems
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <FILE>.o - Builds <FILE>.o object file
#      build - Builds and links all source files
#      all - Same as build
#      clean - removes all generated files
#
# Platform Overrides:
#      CPU - ARM Cortex Architecture (cortex-m4)
#      ARCH - ARM Architecture (arm, thumb)
#      SPECS - Specs file to give the linker (nosys.specs, nano.specs)
#
#------------------------------------------------------------------------------
include sources.mk


TARGET = c1m2

ifeq ($(PLATFORM),HOST) 
	#FOR HOST MACHINE(LINUX)
	
		CC = gcc
		#Utilities
		LD = ld
		SIZE = size
		OBJDUMP = objdump

		# Additional Flags 
		LDFLAGS = -Wl,-Map=$(TARGET).map


	else 
	#FOR MSP432(ARM)

		CC = arm-none-eabi-gcc
		#Utilities
		LD = arm-none-eabi-ld
		OBJDUMP = arm-none-eabi-objdump
		SIZE = arm-none-eabi-size

		# Architecture Specific Flags for MSP432(ARM)
		CPU = cortex-m4
		ARCH = thumb
		SPECS = nosys.specs
		FLOAT-ABI = hard
		FPU = fpv4-sp-d16

		# Platform Specific Flags
		LINKER_FILE = ../msp432p401r.lds
		
		# Additional Flags and Defines
		LDFLAGS = -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
		ARMFLAGS = -mcpu=$(CPU) -m$(ARCH) -march=armv7e-m -mfloat-abi=$(FLOAT-ABI) -mfpu=$(FPU) --specs=$(SPECS) 

	endif

#Compiler Flags and Defines

CFLAGS = -Wall -Werror -g -O0 -std=c99 -D$(PLATFORM) $(ARMFLAGS)


#for Object file
OBJS = $(SOURCES:.c=.o)

#for PreProcessored file 
PP = $(SOURCES:.c=.i)

#for Assembler file
AS = $(SOURCES:.c=.asm)

#for Dependency Files
DEP = $(SOURCES:.c=.d)

#memory.* and main.* other files are getting deleted.  
FILES = *.asm *.i *.o *.d


%.o : %.c 
		$(CC) $(INCLUDES) -c $< $(CFLAGS) -o $@

%.i : %.c 
		$(CC) $(INCLUDES) -E $< $(CFLAGS) -o $@

%.asm : %.c 
		$(CC) $(INCLUDES) -S $< $(CFLAGS) -o $@

$(TARGET).asm : $(TARGET).out
		$(OBJDUMP) -d $(TARGET).out >> $@

%.d : %.c 
		$(CC) $(INCLUDES) -M $< $(CFLAGS) -o $(TARGET).o


.PHONY: compile-all
compile-all: $(OBJS)
	$(CC) $(INCLUDES) $(OBJS) -c $(CFLAGS) -o $(TARGET).o

.PHONY: build
build: $(TARGET).out $(TARGET).asm

$(TARGET).out: $(OBJS) $(DEP)
		$(CC) $(CFLAGS) $(INCLUDES) $(LDFLAGS) -o $@ $(OBJS)
		$(SIZE) -Atd $(TARGET).out

.PHONY: clean
clean:
		rm -f $(TARGET).asm $(FILES) $(TARGET).out $(TARGET).map $(PP) $(AS) $(DEP) $(OBJS)

