#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id$

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/kernel-defaults.mk

PKG_NAME:=RTL8814A
PKG_VERSION=2016-10-20-$(PKG_SOURCE_VERSION)
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/weedy/rtl8812AU.git
PKG_SOURCE_VERSION:=a422338714853794b7cfb8ed7e2fcec355b4399d
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz


PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8814au
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for RTL8814AU wireless chipsets
  DEPENDS:= @USB_SUPPORT +kmod-usb-core +kmod-mac80211
  VERSION:=$(LINUX_VERSION)+$(PKG_VERSION)
  FILES:= $(PKG_BUILD_DIR)/8814au.ko
#  AUTOLOAD:=$(call AutoLoad,rtl8814au)
endef

define Build/Compile
	$(MAKE) $(KERNEL_MAKEOPTS) M=$(PKG_BUILD_DIR) \
		USER_EXTRA_CFLAGS="-D_LINUX_BYTEORDER_SWAB_H -DCONFIG_BIG_ENDIAN -DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT" \
		CONFIG_RTL8814A=y CONFIG_RTL8814AU=m \
		modules
endef

$(eval $(call KernelPackage,rtl8814au))
