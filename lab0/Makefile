CC = aarch64-linux-gnu-gcc
LD = aarch64-linux-gnu-ld
OBJCOPY = aarch64-linux-gnu-objcopy
OBJDUMP = aarch64-linux-gnu-objdump

CFLAGS = -g
LDFLAGS = -T linker.ld

.PHONY: all clean run debug disasm

all: kernel8.img

a.o: a.S
	$(CC) $(CFLAGS) -c $< -o $@

kernel8.elf: a.o linker.ld
	$(LD) $(LDFLAGS) -o $@ a.o

kernel8.img: kernel8.elf
	$(OBJCOPY) -O binary $< $@

run: kernel8.img
	qemu-system-aarch64 -M raspi3b -kernel $< -nographic

debug: kernel8.img
	qemu-system-aarch64 -M raspi3b -kernel $< -nographic -S -gdb tcp:127.0.0.1:1234

disasm: kernel8.elf
	$(OBJDUMP) -d $<

clean:
	rm -f a.o kernel8.elf kernel8.img
