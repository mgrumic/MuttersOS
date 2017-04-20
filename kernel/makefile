OBJS:=boot.o kernel.o

ARCH ?=
CROSS_COMPILE ?=

CFLAGS:=
CC:=$(CROSS_COMPILE)gcc

CRTI_OBJ=crti.o
CRTBEGIN_OBJ:=$(shell $(CC) $(CFLAGS) -print-file-name=crtbegin.o)
CRTEND_OBJ:=$(shell $(CC) $(CFLAGS) -print-file-name=crtend.o)
CRTN_OBJ=crtn.o

OBJ_LINK_LIST:=$(CRTI_OBJ) $(CRTBEGIN_OBJ) $(OBJS) $(CRTEND_OBJ) $(CRTN_OBJ)
INTERNAL_OBJS=$(CRTI_OBJ) $(OBJS) $(CRTN_OBJ)

%.o : %.s
	nasm -felf32 $< -o $@

%.o : %.c
	$(CC) -c $< -o $@ -std=gnu99 -ffreestanding -O2 -Wall -Wextra

all: $(INTERNAL_OBJS)
	$(CC) -T linker.ld -o myos.bin $(OBJ_LINK_LIST) -ffreestanding -O2 -nostdlib -lgcc

clean:
	rm -f myos.bin $(INTERNAL_OBJS)
