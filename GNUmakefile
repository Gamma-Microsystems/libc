LIBC_OBJS  = $(patsubst %.c,%.o,$(wildcard *.c))
LIBC_OBJS += $(patsubst %.c,%.o,$(wildcard */*.c))
LIBC_OBJS += $(patsubst %.c,%.o,$(wildcard arch/$(KARCH)/*.c))
KARCH = x86_64
CC = $(KARCH)-elf-gcc
CFLAGS := -Os -std=gnu11 -ffreestanding -Wall -Wextra -Wno-unused-parameter
AR = $(KARCH)-elf-ar
CRTS = ../base/lib/crt0.o ../base/lib/crti.o ../base/lib/crtn.o

../base/lib/libc.a: $(LIBC_OBJS) $(CRTS)
	@$(AR) cr $@ $(LIBC_OBJS)

../base/lib/libc.so: $(LIBC_OBJS) | $(CRTS)
	$(CC) -nodefaultlibs -shared -fPIC -o $@ $^ -lgcc
