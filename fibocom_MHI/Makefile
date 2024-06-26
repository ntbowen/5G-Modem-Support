#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pcie_mhi_fb
PKG_VERSION:=3.2
PKG_RELEASE:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/pcie_mhi_fb
  SUBMENU:=WWAN Support
  TITLE:=Kernel pcie driver for MHI device
  DEPENDS:=+pciids +pciutils +fibocom-dial
  FILES:=$(PKG_BUILD_DIR)/pcie_mhi_fb.ko
  AUTOLOAD:=$(call AutoLoad,90,pcie_mhi_fb)
endef

define KernelPackage/pcie_mhi_fb/description
  Kernel module for register a custom pciemhi platform device.
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	M="$(PKG_BUILD_DIR)" \
	$(EXTRA_KCONFIG)

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		M=$(PKG_BUILD_DIR) \
		modules
endef

define KernelPackage/pcie_mhi_fb/install
	$(INSTALL_DIR) $(1)/etc/modules.d
	echo pcie_mhi_fb > $(1)/etc/modules.d/pcie_mhi_fb
endef

$(eval $(call KernelPackage,pcie_mhi_fb))
