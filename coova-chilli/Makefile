#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=coova-chilli
PKG_VERSION:=1.3.1.3
PKG_MAINTAINER:=Imre Kaloz <kaloz@openwrt.org>
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING
PKG_RELEASE:=2

PKG_SOURCE_URL:=https://github.com/coova/coova-chilli/archive/
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_MD5SUM:=09df3a3baf4319b20ec2b2a3135d7558

PKG_INSTALL:=1

PKG_CONFIG_DEPENDS := \
  COOVACHILLI_ACCOUNTING_ONOFF \
  COOVACHILLI_BINSTATUSFILE \
  COOVACHILLI_CHILLIQUERY \
  COOVACHILLI_COA \
  COOVACHILLI_CONFIG_ATTRIBUTE \
  COOVACHILLI_CURL \
  COOVACHILLI_CYASSL \
  COOVACHILLI_DEBUG \
  COOVACHILLI_DEBUG2 \
  COOVACHILLI_DHCPOPT \
  COOVACHILLI_DHCPRADIUS \
  COOVACHILLI_DNSLOG \
  COOVACHILLI_FORCEDNS \
  COOVACHILLI_IEEE8021Q \
  COOVACHILLI_IEEE8023 \
  COOVACHILLI_JSON \
  COOVACHILLI_LARGELIMITS \
  COOVACHILLI_LAYER3 \
  COOVACHILLI_LEAKYBUCKET \
  COOVACHILLI_LOCATION \
  COOVACHILLI_MATRIXSSL \
  COOVACHILLI_MINICONFIG \
  COOVACHILLI_MINIPORTAL \
  COOVACHILLI_MMAP \
  COOVACHILLI_NETBIOS \
  COOVACHILLI_NETNAT \
  COOVACHILLI_NFQUEUE \
  COOVACHILLI_NOSSL \
  COOVACHILLI_OPENSSL \
  COOVACHILLI_POLL \
  COOVACHILLI_PROXY \
  COOVACHILLI_RADPROXY \
  COOVACHILLI_REDIR \
  COOVACHILLI_REDIRINJECT \
  COOVACHILLI_RTMON \
  COOVACHILLI_SESSIONPROXY \
  COOVACHILLI_STATUSFILE \
  COOVACHILLI_TAP \
  COOVACHILLI_UAMANYIP \
  COOVACHILLI_UAMDOMAINFILE \
  COOVACHILLI_UAMUIPORT \
  COOVACHILLI_USERAGENT \
  COOVACHILLI_WPAD

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/coova-chilli
  SUBMENU:=Captive Portals
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-tun +librt +COOVACHILLI_MINIPORTAL:haserl +COOVACHILLI_MATRIXSSL:libmatrixssl +COOVACHILLI_CYASSL:libcyassl +COOVACHILLI_OPENSSL:libopenssl +COOVACHILLI_CURL:libcurl +COOVACHILLI_NFQUEUE:libnetfilter-queue
  TITLE:=Wireless LAN HotSpot controller (Coova Chilli Version)
  URL:=http://www.coova.org/CoovaChilli
  MENU:=1
endef

define Package/coova-chilli/description
	CoovaChilli is an open source access controller for wireless LAN
	access points and is based on ChilliSpot. It is used for authenticating
	users of a wireless (or wired) LAN. It supports web based login (UAM)
	which is today's standard for public HotSpots and it supports Wireless
	Protected Access (WPA) which is the standard of the future.
	Authentication,	authorization and accounting (AAA) is handled by your
	favorite radius server.
endef

define Package/coova-chilli/config
  source "$(SOURCE)/Config.in"
endef

define KernelPackage/ipt-coova
  URL:=http://www.coova.org/CoovaChilli
  SUBMENU:=Netfilter Extensions
  DEPENDS:=coova-chilli +kmod-ipt-core +libxtables
  TITLE:=Coova netfilter module
  FILES:=$(PKG_BUILD_DIR)/src/linux/xt_*.$(LINUX_KMOD_SUFFIX)
  AUTOLOAD:=$(call AutoProbe,xt_coova)
endef

define KernelPackage/ipt-coova/description
	Netfilter kernel module for CoovaChilli
	Includes:
	- coova
endef

DISABLE_NLS=

TARGET_CFLAGS += $(FPIC)

CONFIGURE_VARS += \
       ARCH="$(LINUX_KARCH)" \
       KERNEL_DIR="$(LINUX_DIR)"

MAKE_FLAGS += \
       ARCH="$(LINUX_KARCH)" \
       KERNEL_DIR="$(LINUX_DIR)"

MAKE_INSTALL_FLAGS += \
       ARCH="$(LINUX_KARCH)" \
       KERNEL_DIR="$(LINUX_DIR)" \
       INSTALL_MOD_PATH="$(PKG_INSTALL_DIR)"

define Build/Prepare
$(call Build/Prepare/Default)
	( cd $(PKG_BUILD_DIR) ; \
		[ -f ./configure ] || { \
			./bootstrap ; \
		} \
	)
endef

define Build/Configure
	$(call Build/Configure/Default, \
	$(if $(CONFIG_COOVACHILLI_ACCOUNTING_ONOFF),,--disable-accounting-onoff) \
	$(if $(CONFIG_COOVACHILLI_BINSTATUSFILE),--enable-binstatusfile) \
	$(if $(CONFIG_COOVACHILLI_CHILLIQUERY),,--disable-chilliquery) \
	$(if $(CONFIG_COOVACHILLI_COA),--enable-coa) \
	$(if $(CONFIG_COOVACHILLI_CONFIG_ATTRIBUTE),,--disable-coovachilliconfig) \
	$(if $(CONFIG_COOVACHILLI_CURL),--with-curl) \
	$(if $(CONFIG_COOVACHILLI_CYASSL),--with-cyassl) \
	$(if $(CONFIG_COOVACHILLI_DEBUG),,--disable-debug) \
	$(if $(CONFIG_COOVACHILLI_DEBUG2),--enable-debug2) \
	$(if $(CONFIG_COOVACHILLI_DHCPOPT),--enable-dhcpopt) \
	$(if $(CONFIG_COOVACHILLI_DHCPRADIUS),,--disable-dhcpradius) \
	$(if $(CONFIG_COOVACHILLI_DNSLOG),--enable-dnslog) \
	$(if $(CONFIG_COOVACHILLI_FORCEDNS),--enable-forcedns) \
	$(if $(CONFIG_COOVACHILLI_IEEE8021Q),,--disable-ieee8021q) \
	$(if $(CONFIG_COOVACHILLI_IEEE8023),--enable-ieee8023) \
	$(if $(CONFIG_COOVACHILLI_JSON),--enable-libjson,--disable-json) \
	$(if $(CONFIG_COOVACHILLI_LARGELIMITS),--enable-largelimits) \
	$(if $(CONFIG_COOVACHILLI_LAYER3),--enable-layer3) \
	$(if $(CONFIG_COOVACHILLI_LEAKYBUCKET),,--disable-leakybucket) \
	$(if $(CONFIG_COOVACHILLI_LOCATION),--enable-location) \
	$(if $(CONFIG_COOVACHILLI_MATRIXSSL),--with-matrixssl) \
	$(if $(CONFIG_COOVACHILLI_MINICONFIG),--enable-miniconfig) \
	$(if $(CONFIG_COOVACHILLI_MINIPORTAL),--enable-miniportal) \
	$(if $(CONFIG_COOVACHILLI_MMAP),--with-mmap) \
	$(if $(CONFIG_COOVACHILLI_NETBIOS),--enable-netbios) \
	$(if $(CONFIG_COOVACHILLI_NETNAT),--enable-netnat) \
	$(if $(CONFIG_COOVACHILLI_NFQUEUE),--with-nfqueue) \
	$(if $(CONFIG_COOVACHILLI_OPENSSL),--with-openssl) \
	$(if $(CONFIG_COOVACHILLI_POLL),--with-poll) \
	$(if $(CONFIG_COOVACHILLI_PROXY),--enable-chilliproxy) \
	$(if $(CONFIG_COOVACHILLI_RADPROXY),,--disable-radproxy) \
	$(if $(CONFIG_COOVACHILLI_REDIR),--enable-chilliredir) \
	$(if $(CONFIG_COOVACHILLI_REDIRINJECT),--enable-redirinject) \
	$(if $(CONFIG_COOVACHILLI_RTMON),--enable-rtmon) \
	$(if $(CONFIG_COOVACHILLI_SESSIONPROXY),--enable-sessproxy) \
	$(if $(CONFIG_COOVACHILLI_STATUSFILE),--enable-statusfile) \
	$(if $(CONFIG_COOVACHILLI_TAP),,--disable-tap) \
	$(if $(CONFIG_COOVACHILLI_UAMANYIP),,--disable-uamanyip) \
	$(if $(CONFIG_COOVACHILLI_UAMDOMAINFILE),--enable-uamdomainfile) \
	$(if $(CONFIG_COOVACHILLI_UAMUIPORT),,--disable-uamuiport) \
	$(if $(CONFIG_COOVACHILLI_USERAGENT),--enable-useragent) \
	$(if $(CONFIG_COOVACHILLI_WPAD),--enable-wpad) \
	$(if $(CONFIG_PACKAGE_kmod-ipt-coova),--with-nfcoova) \
	)
endef

define Package/coova-chilli/conffiles
/etc/config/chilli
endef

define Package/coova-chilli/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/chilli.conf $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/chilli
	$(CP) $(PKG_INSTALL_DIR)/etc/chilli/* $(1)/etc/chilli/
	$(RM) $(1)/etc/chilli/gui-config-default.ini
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/etc/chilli/defaults $(1)/etc/chilli/
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./files/chilli.hotplug $(1)/etc/hotplug.d/iface/30-chilli
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/chilli* $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/chilli.init $(1)/etc/init.d/chilli
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) files/chilli.config $(1)/etc/config/chilli
	$(INSTALL_DIR) $(1)/lib/firewall
	$(CP) files/chilli.firewall $(1)/lib/firewall/chilli.sh
endef

define KernelPackage/ipt-coova/install
	$(INSTALL_DIR) $(1)/usr/lib/iptables
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/iptables/lib*.so $(1)/usr/lib/iptables/
endef

$(eval $(call BuildPackage,coova-chilli))
$(eval $(call KernelPackage,ipt-coova))
