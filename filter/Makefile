TOOLCHAIN_PATH = /opt/fsl-imx-x11/4.1.15-2.0.0/sysroots/x86_64-pokysdk-linux/usr/bin/arm-poky-linux
CFLAGS = -march=armv7-a -mfpu=neon  -mfloat-abi=hard -mcpu=cortex-a9 -Wall
SYSROOT_PATH = /opt/fsl-imx-x11/4.1.15-2.0.0/sysroots/cortexa9hf-neon-poky-linux-gnueabi
CC =$(TOOLCHAIN_PATH)/arm-poky-linux-gcc $(CLFAGS) --sysroot=$(SYSROOT_PATH)
CXX =$(TOOLCHAIN_PATH)/arm-poky-linux-g++ $(CLFAGS) --sysroot=$(SYSROOT_PATH)
CPP = $(TOOLCHAIN_PATH)/arm-poky-linux-gcc -E $(CLFAGS) --sysroot=$(SYSROOT_PATH)
LD = $(TOOLCHAIN_PATH)/arm-poky-linux-gnu-ld --sysroot=$(SYSROOT_PATH)

CFLAGS+= -g
LDFLAGS= -lpthread -lglib-2.0 -lgobject-2.0 -lrt -lgstreamer-1.0 -lgstfft-1.0 -lm #-lmicrohttpd
TARGET_ROOTFS = ./

BUILDFLAGS=\
-I$(SYSROOT_PATH)/usr/include \
-I$(SYSROOT_PATH)/usr/src/kernel/include/uapi \
-I$(SYSROOT_PATH)/usr/include \
-I$(SYSROOT_PATH)/usr/src/kernel/include \
-I$(SYSROOT_PATH)/usr/src/kernel/arch/arm/include \
-I$(SYSROOT_PATH)/usr/include/glib-2.0 \
-I$(SYSROOT_PATH)/usr/include/gstreamer-1.0 \
-I$(SYSROOT_PATH)/usr/lib/gstreamer-1.0/include \
-I$(SYSROOT_PATH)/usr/lib/glib-2.0/include \
-L./

all: filter

filter: filter.o 
	$(CC) $(CFLAGS) $(BUILDFLAGS) $(LDFLAGS) filter.o  -o $@
filter.o: filter.c
	$(CC) -c $(BUILDFLAGS) $(CFLAGS) $< -o $@
#callbacks.o: callbacks.c
#        $(CC) -c $(BUILDFLAGS) $(CFLAGS) $< -o $@
#main.o: main.c
#        $(CC) -c $(BUILDFLAGS) $(CFLAGS) $< -o $@
#httpserver.o: httpserver.c
#        $(CC) -c $(BUILDFLAGS) $(CFLAGS) $< -o $@
#mqueue: mqueue_client.c
#        $(CC) $(CFLAGS) $(BUILDFLAGS) $(LDFLAGS) $< -o $@
clean:
	rm -f *.o
