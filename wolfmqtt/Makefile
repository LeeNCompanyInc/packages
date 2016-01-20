#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfmqtt
PKG_VERSION:=0.4
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0+

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfMQTT/releases/download/v$(PKG_VERSION)/
PKG_MD5SUM:=351dc6f95f636c2f5779f70ad4204500

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libwolfmqtt
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libcyassl
	TITLE:=libwolfmqtt - an MQTT client library
	URL:=https://www.wolfssl.com/wolfSSL/Products-wolfmqtt.html
endef

define Package/libwolfmqtt/description
wolfMQTT is an MQTT client library integrates with wolfSSL
endef

TARGET_CFLAGS += $(FPIC)

define Build/Prepare
	$(call Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR) ; \
		[ -f ./configure ] || { \
			./autogen.sh ; \
		} \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwolfmqtt.{so*,la} $(1)/usr/lib/
endef

define Package/libwolfmqtt/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwolfmqtt.{so*,la} $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libwolfmqtt))
