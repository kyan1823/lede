#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id$

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=cryptodev-linux
PKG_VERSION:=1.14
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://codeload.github.com/$(PKG_NAME)/$(PKG_NAME)/tar.gz/$(PKG_NAME)-$(PKG_VERSION)?
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=67223d5bee4749028e78e87372cee3bca79d9a20f7b6cb915aa080c59d2a2d98
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Ansuel Smith <ansuelsmth@gmail.com>

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define KernelPackage/cryptodev
  SUBMENU:=Cryptographic API modules
  TITLE:=Driver for cryptographic acceleration
  URL:=https://github.com/cryptodev-linux/cryptodev-linux
  DEPENDS:=+kmod-crypto-authenc +kmod-crypto-hash
  FILES:=$(PKG_BUILD_DIR)/cryptodev.$(LINUX_KMOD_SUFFIX)
  AUTOLOAD:=$(call AutoLoad,50,cryptodev)
  MODPARAMS.cryptodev:=cryptodev_verbosity=-1
endef

define KernelPackage/cryptodev/description
  This is a driver for that allows to use the Linux kernel supported
  hardware ciphers by user-space applications.
endef

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(KERNEL_MAKE_FLAGS) \
		KERNEL_DIR="$(LINUX_DIR)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/crypto
	$(CP) $(PKG_BUILD_DIR)/crypto/cryptodev.h $(STAGING_DIR)/usr/include/crypto/
endef

$(eval $(call KernelPackage,cryptodev))
