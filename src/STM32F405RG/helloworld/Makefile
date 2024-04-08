include ../makefile.conf
include $(BASE)/imports.mak

NAME=helloworld
STARTUP_DEFS=

LDSCRIPTS=-L. -T ../$(DEVICE).ld
LFLAGS=$(USE_NANO) $(USE_SEMIHOST) $(LDSCRIPTS) $(GC) $(MAP)

$(NAME).axf: $(NAME).c $(STARTUP)
	$(CC) $^ $(CFLAGS) $(LFLAGS) -o $@

clean:
	@ echo Cleaning...
	@ $(RM) $(NAME).axf > $(DEVNULL) 2>&1
	@ $(RM) $(NAME).map > $(DEVNULL) 2>&1
