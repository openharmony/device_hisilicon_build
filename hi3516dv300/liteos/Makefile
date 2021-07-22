
LITEOSTOPDIR := $(shell pwd)/../../../../../kernel/liteos_a
CONFIG_FILE := $(LITEOSTOPDIR)/.config

ifneq ($(wildcard $(OUTDIR)/obj/kernel/liteos_a/liteos.ninja), )
LITEOS_MENUCONFIG_H := $(OUTDIR)/config.h
CONFIG_FILE := $(OUTDIR)/config.gni
liteos_libdep := $(shell sed 's,|.*,,g' $(OUTDIR)/obj/kernel/liteos_a/liteos.ninja | tr '\n' ' '| tr '=' ' '| tr '|' ' ' | tr ':' ' ')
liteos_libdep := $(sort $(filter %.a,$(liteos_libdep)))
liteos_libdep := $(patsubst ./libs/lib%.a,-l%,$(liteos_libdep))
liteos_libdep := $(patsubst ../%,$(OUTDIR)/../%,$(liteos_libdep))
liteos_ldflags := -L$(OUTDIR) -L$(OUTDIR)/libs
else ifeq ($(wildcard $(CONFIG_FILE)), )
$(error  "########################kernel is not compiled################################")
endif
include $(LITEOSTOPDIR)/config.mk

ifeq ($(LOSCFG_COMPILER_CLANG_LLVM), y)
MPP_DIR := $(LITEOSTOPDIR)/../../device/hisilicon/hispark_taurus/sdk_liteos/mpp/module_init/
else ifeq ($(LOSCFG_COMPILER_HIMIX_32), y)
MPP_DIR := $(LITEOSTOPDIR)/../../device/hisilicon/hi3516dv300/sdk_liteos/mpp/
else
$(error  "########################compiler is not supported################################")
endif

LITEOS_LIBDEP := $(or $(liteos_libdep),$(LITEOS_LIBDEP))
LITEOS_LDFLAGS := $(liteos_ldflags) $(LITEOS_LDFLAGS)

include hi3516dv300.mak
