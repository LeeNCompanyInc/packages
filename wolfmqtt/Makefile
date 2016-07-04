#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wolfmqtt
PKG_VERSION:=v0.8
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0+

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/wolfSSL/wolfMQTT.git
PKG_SOURCE_VERSION:=11625f952f8885a6669357b494b24fe4843563be

PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=libcyassl
PKG_BUILD_PARALLEL:=0

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

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--disable-examples

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
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwolfmqtt.so* $(1)/usr/lib/
endef

define Package/libwolfmqtt/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libwolfmqtt.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libwolfmqtt))
