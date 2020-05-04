################################################################################
#
# 8821cu is the Linux device driver released for Realtek 2.5Gigabit Ethernet
# controllers with PCI-Express interface.
#
# Copyright(c) 2018 Realtek Semiconductor Corp. All rights reserved.
#
# This program is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by the Free
# Software Foundation; either version 2 of the License, or (at your option)
# any later version.
#
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
# FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for
# more details.
#
# You should have received a copy of the GNU General Public License along with
# this program; if not, see <http://www.gnu.org/licenses/>.
#
# Author:
# Realtek NIC software team <nicfae@realtek.com>
# No. 2, Innovation Road II, Hsinchu Science Park, Hsinchu 300, Taiwan
#
################################################################################

################################################################################
#  This product is covered by one or more of the following patents:
#  US6,570,884, US6,115,776, and US6,327,625.
################################################################################

#KFLAG := 2$(shell uname -r | sed -ne 's/^2\.[4]\..*/4/p')x

#all: clean modules install

#modules:
#ifeq ($(KFLAG),24x)
#	$(MAKE) -C src/ -f Makefile_linux24x modules
#else
#	$(MAKE) -C src/ modules
#endif

#clean:
#ifeq ($(KFLAG),24x)
#	$(MAKE) -C src/ -f Makefile_linux24x clean
#else
#	$(MAKE) -C src/ clean
#endif

#install:
#ifeq ($(KFLAG),24x)
#	$(MAKE) -C src/ -f Makefile_linux24x install
#else
#	$(MAKE) -C src/ install
#endif



# Attribution: https://gist.github.com/lenew/9b41ba901c3393047ede0766760f9d55

#Put this source to 'package/kernel/8821cu' folder of OpenWRT/LEDE SDK
#Build(make menuconfig, make defconfig, make)

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=8821cu
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/axiomware/RTL8821CU_driver_v5.8.1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2020-01-12
PKG_SOURCE_VERSION:=978fa97543cd0b2cc32e7e8e075f4e92af632554

include $(INCLUDE_DIR)/package.mk

define KernelPackage/8821cu
  TITLE:=Driver for Realtek rtl8811cu/8821cu chipsets
  SUBMENU:=Network Devices
  VERSION:=$(LINUX_VERSION)+$(PKG_VERSION)-$(BOARD)-$(PKG_RELEASE)
  FILES:= $(PKG_BUILD_DIR)/8821cu.ko
  AUTOLOAD:=$(call AutoProbe,8821cu)
endef

define Package/8821cucu/description
 This package contains a driver for Realtek 8821cu chipsets.
endef

8821cu_MAKEOPTS= -C $(LINUX_DIR) \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		PATH="$(TARGET_PATH)" \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		TARGET="$(HAL_TARGET)" \
		TOOLPREFIX="$(KERNEL_CROSS)" \
		TOOLPATH="$(KERNEL_CROSS)" \
		KERNELPATH="$(LINUX_DIR)" \
		KERNELDIR="$(LINUX_DIR)" \
		LDOPTS=" " \
		DOMULTI=1

define Build/Compile
	$(MAKE) $(8821cu_MAKEOPTS) modules
endef

$(eval $(call KernelPackage,8821cu))
