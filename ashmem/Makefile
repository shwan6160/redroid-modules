ccflags-y += -I$(src)
obj-m := ashmem_linux.o
ashmem_linux-y := ashmem.o deps.o

KDIR ?= /lib/modules/`uname -r`/build
INSTALL_MOD_DIR ?= /lib/modules/`uname -r`/extra

all:
	$(MAKE) -C $(KDIR) M=$$PWD

install: all
	mkdir -p $(INSTALL_MOD_DIR)
	cp ashmem_linux.ko $(INSTALL_MOD_DIR)
	depmod -a
	modprobe ashmem_linux

modules_install:
	$(MAKE) -C $(KDIR) M=$$PWD modules_install

uninstall:
	rmmod ashmem_linux

clean:
	$(MAKE) -C $(KDIR) M=$$PWD clean

