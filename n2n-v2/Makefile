#
# Copyright (C) 2007-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_BRANCH:=master
PKG_SOURCE_URL:=git://github.com/lukablurr/n2n_v2_fork
PKG_REV:=d3bc1d5a81b22637d6ec5cb2712f3bbfa6232b27

PKG_NAME:=n2n-v2
PKG_VERSION:=$(PKG_REV)
PKG_RELEASE:=1

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_CONFIG_DEPENDS := \
	CONFIG_N2N_AES_ENCRYPTION

CMAKE_INSTALL := 1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/n2n-v2
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VPN tunneling daemon
  URL:=http://www.ntop.org/n2n/
  SUBMENU:=VPN
  DEPENDS:=+libc +libpthread +kmod-tun +CONFIG_N2N_AES_ENCRYPTION:libopenssl
endef

define Package/n2n-v2/config
	source "$(SOURCE)/Config.in"
endef

ifneq ($(CONFIG_N2N_AES_ENCRYPTION),y)
  CMAKE_OPTIONS += -DN2N_OPTION_AES=no
endif

define Package/n2n-v2/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/edge $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/supernode $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/n2n_v2.config $(1)/etc/config/n2n
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/n2n_v2.init $(1)/etc/init.d/n2n
endef

define Package/n2n-v2/conffiles
/etc/config/n2n
endef

$(eval $(call BuildPackage,n2n-v2))
