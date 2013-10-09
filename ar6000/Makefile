#ar6000
obj-m += ar6000.o

ar6000-y += debug.o debugfs_pri.o hif.o htc.o bmi.o cfg80211.o
ar6000-y += cfg80211_btcoex.o pm.o init.o main.o txrx.o wmi.o wmi_btcoex.o
ar6000-y += sdio.o platform.o softmac.o wmiconfig.o testmode.o
ar6000-y += recovery.o

ccflags-y += -D__CHECK_ENDIAN__
ccflags-y += -DCONFIG_ATH6KL_DEBUG
ccflags-y += -DCONFIG_CFG80211
ccflags-y += -DCONFIG_CFG80211_DEFAULT_PS
ccflags-y += -DCONFIG_CFG80211_WEXT
ccflags-y += -DCONFIG_NL80211_TESTMODE

ATH_ROOT = $(src)/..

ccflags-y += -I$(ATH_ROOT)/include
ccflags-y += -I$(ATH_ROOT)/ar6000
ccflags-y += -include $(ATH_ROOT)/include/linux/ieee80211.h
ccflags-y += -include $(ATH_ROOT)/include/linux/nl80211.h
ccflags-y += -include $(ATH_ROOT)/include/net/cfg80211.h
ccflags-y += -include $(ATH_ROOT)/include/linux/compat-2.6.h

ldflags-y += --strip-debug

KBUILD_EXTRA_SYMBOLS = $(ATH_ROOT)/cfg80211/Module.symvers

all:
	$(MAKE) modules
	$(MAKE) clean

modules:
	$(MAKE) -C $(KERNEL_OUT) M=`pwd` ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) modules
	mv ar6000.ko $(OUTPUT_FILE)

clean:
	$(MAKE) -C $(KERNEL_OUT) M=`pwd` ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) clean