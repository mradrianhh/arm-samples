include ../makefile.conf
include $(BASE)/imports.mak

NAME=main

OBJECTS = $(NAME).obj $(SYSTEM_OBJ) $(STARTUP_OBJ)

CFLAGS = -I.. \
	-I$(BASE)/msp432p401r_sdk \
	-I$(BASE)/msp432p401r_sdk/third_party/CMSIS/Include \
    -D__MSP432P401R__ \
    -DDeviceFamily_MSP432P401x \
    -mcpu=cortex-m4 \
    -march=armv7e-m \
    -mthumb \
    -std=c99 \
    -mfloat-abi=hard \
    -mfpu=fpv4-sp-d16 \
    -ffunction-sections \
    -fdata-sections \
    -ggdb \
    -gstrict-dwarf \
    -Wall \
    -I$(GCC_PATH)/arm-none-eabi/include/newlib-nano \
    -I$(GCC_PATH)/arm-none-eabi/include

LFLAGS = -Wl,-T,../MSP432P401R.ld \
    -Wl,-Map,$(NAME).map \
    -L$(BASE)/msp432p401r_sdk \
	-l:ti/display/lib/display.am4fg \
    -l:ti/grlib/lib/gcc/m4f/grlib.a \
    -l:third_party/spiffs/lib/gcc/m4f/spiffs.a \
    -l:ti/drivers/lib/drivers_msp432p401x.am4fg \
    -l:third_party/fatfs/lib/gcc/m4f/fatfs.a \
    -l:ti/devices/msp432p4xx/driverlib/gcc/msp432p4xx_driverlib.a \
    -march=armv7e-m \
    -mthumb \
    -mfloat-abi=hard \
    -mfpu=fpv4-sp-d16 \
    -static \
    -Wl,--gc-sections \
    -lgcc \
    -lc \
    -lm \
    -lnosys \
    --specs=nano.specs

all: $(NAME).axf

$(NAME).obj: $(NAME).c
	@ echo Building $@
	@ $(CC) $(CFLAGS) $< -c -o $@

$(SYSTEM_OBJ): $(SYSTEM_SRC)
	@ echo Building $@
	@ $(CC) $(CFLAGS) $< -c -o $@

$(STARTUP_OBJ): $(STARTUP_SRC)
	@ echo Building $@
	@ $(CC) $(CFLAGS) $< -c -o $@

$(NAME).axf: $(OBJECTS)
	@ echo linking $@
	@ $(CC)  $(OBJECTS)  $(LFLAGS) -o $(NAME).axf

clean:
	@ echo Cleaning...
	@ $(RM) $(OBJECTS) > $(DEVNULL) 2>&1
	@ $(RM) $(NAME).axf > $(DEVNULL) 2>&1
	@ $(RM) $(NAME).map > $(DEVNULL) 2>&1
