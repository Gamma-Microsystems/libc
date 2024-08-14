LIBC_OBJS  = $(patsubst %.c,%.o,$(wildcard *.c))
LIBC_OBJS += $(patsubst %.c,%.o,$(wildcard */*.c))
LIBC_OBJS += $(patsubst %.c,%.o,$(wildcard arch/$(KARCH)/*.c))
KARCH = x86_64
CC = $(KARCH)-elf-gcc
CFLAGS := -Os -std=gnu11 -ffreestanding -Wall -Wextra -Wno-unused-parameter
AR = $(KARCH)-elf-ar
AS = $(KARCH)-elf-as
CRTS = ../base/lib/crt0.o ../base/lib/crti.o ../base/lib/crtn.o

%.o: %.c ../base/usr/include/syscall.h 
	$(CC) $(CFLAGS) -fPIC -c -o $@ $<

../base/lib/libc.a: $(LIBC_OBJS) $(CRTS)
	@echo -e 'AR'
	@$(AR) cr $@ $(LIBC_OBJS)

../base/lib/libc.so: $(LIBC_OBJS) | $(CRTS)
	@echo -e 'CC'
	@$(CC) -nodefaultlibs -shared -fPIC -o $@ $^ -lgcc

../base/lib/crt%.o: arch/$(KARCH)/crt%.S
	$(AS) -o $@ $<

../base/lib/libm.so: ../util/libm.c
	$(CC) -shared -nostdlib -fPIC -o $@ $<
