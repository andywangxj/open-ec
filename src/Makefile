##
## This file is part of anlogic-usbjtag project
##
## Copyright (C) 2009 Uwe Hermann <uwe@hermann-uwe.de>
## Copyright (C) 2017 Zhiyuan Wan <h@iloli.bid>
##
## This library is free software: you can redistribute it and/or modify
## it under the terms of the GNU Lesser General Public License as published by
## the Free Software Foundation, either version 3 of the License, or
## (at your option) any later version.
##
## This library is distributed in the hope that it will be useful,
## but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU Lesser General Public License for more details.
##
## You should have received a copy of the GNU Lesser General Public License
## along with this library.  If not, see <http://www.gnu.org/licenses/>.
##

BINARY = ec

OBJS = usb_private.o

LDSCRIPT = stm32f103x8.ld

DFU_UTIL = dfu-util
ST_FLASH = st-flash

USB_ID	 = 1d50:6017

LIBNAME		?= opencm3_stm32f1
DEFS		?= -DSTM32F1 -O3
FP_FLAGS    ?= -msoft-float
ARCH_FLAGS	?= -mthumb -mcpu=cortex-m3 $(FP_FLAGS) -mfix-cortex-m3-ldrd

include ../libopencm3.rules.mk


size: $(OBJS) $(BINARY).elf
	@$(PREFIX)-size $(OBJS) $(BINARY).elf
	
dfu:  $(BINARY).bin
	@printf "  FLASH   $<\n"
	@$(DFU_UTIL) -d $(USB_ID) -D $(BINARY).bin -s 0x08002000
stlink: $(BINARY).bin
	@printf "  FLASH   $<\n"
	@$(ST_FLASH) write $(BINARY).bin 0x08002000
