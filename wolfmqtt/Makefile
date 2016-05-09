#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfmqtt
PKG_VERSION:=v0.6
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0+

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfMQTT.git
PKG_SOURCE_VERSION:=449bf467217fd5d57eac068b0db593eeb42447da

PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=libcyassl

include $(INCLUDE_DIR)/package.mk

define Package/libwolfmqtt
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libcyassl +libpthread
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
