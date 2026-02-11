ccflags-y = -I$(src) -DCONFIG_ANDROID_BINDERFS -DCONFIG_ANDROID_BINDER_DEVICES_HACKED="\"binder,hwbinder,vndbinder\""
obj-m := binder_linux.o
binder_linux-y := binderfs.o binder.o binder_alloc.o idr.o deps.o

KDIR ?= /lib/modules/`uname -r`/build
INSTALL_MOD_DIR ?= /lib/modules/`uname -r`/extra 

all:
	$(MAKE) -C $(KDIR) M=$$PWD

install: all
	mkdir -p $(INSTALL_MOD_DIR)
	cp binder_linux.ko $(INSTALL_MOD_DIR)
	depmod -a
	modprobe binder_linux devices="binder,hwbinder,vndbinder"
	mkdir -p /dev/binderfs
	-mount -t binder binder /dev/binderfs
	ln -sf /dev/binderfs/binder /dev/binder
	ln -sf /dev/binderfs/hwbinder /dev/hwbinder
	ln -sf /dev/binderfs/vndbinder /dev/vndbinder

modules_install:
	$(MAKE) -C $(KDIR) M=$$PWD modules_install

uninstall:
	rmmod binder_linux

clean:
	$(MAKE) -C $(KDIR) M=$$PWD clean
	rm *.o.*

