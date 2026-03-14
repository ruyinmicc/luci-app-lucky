# SPDX-License-Identifier: GPL-3.0-only
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lucky
PKG_VERSION:=2.27.2
PKG_RELEASE:=1
PKGARCH:=all 
LUCKY_CONF_DIR := /etc/config/lucky.daji
LUCKY_TMP_BACKUP := /tmp/luckyconfdir

ifeq ($(ARCH),mipsel)
	LUCKY_ARCH:=mipsle_softfloat
endif
ifeq ($(ARCH),mips)
	LUCKY_ARCH:=mips_softfloat
endif
ifeq ($(ARCH),i386)
	LUCKY_ARCH:=i386
endif
ifeq ($(ARCH),x86_64)
	LUCKY_ARCH:=x86_64
endif
ifeq ($(ARCH),arm)
	ifeq ($(BOARD),bcm53xx)
		LUCKY_ARCH:=armv7
	else
		LUCKY_ARCH:=armv7
	endif
endif

# === 注释掉以下冗余且易引发语法错误的嵌套判断块 ===
# ifeq ($(BOARD),bcm53xx)
# 	LUCKY_ARCH:=armv6
# ifeq ($(word 2,$(subst +,$(space),$(call qstrip,$(CONFIG_CPU_TYPE)))),)
# 	LUCKY_ARCH:=armv5
# endif
# endif

ifeq ($(BOARD),kirkwood)
	LUCKY_ARCH:=armv5
endif
ifeq ($(ARCH),aarch64)
	LUCKY_ARCH:=arm64
endif

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=GDY666 <gdy666@foxmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Lucky gdy (wanji custom)
	DEPENDS:=@(i386||x86_64||arm||aarch64||mipsel||mips)
	URL:=https://release.66666.host/
endef

define Package/$(PKG_NAME)/description
  Custom Lucky from wanji: ipv4/ipv6 portforward, ddns, IOT wake on lan, reverse proxy and more...
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	echo "/usr/bin/lucky" > $(PKG_BUILD_DIR)/lucky.keep
	echo "/usr/bin/easytier-cli" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/usr/bin/easytier-core" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/usr/bin/easytier-web" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/usr/bin/AdGuardHome" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/etc/appfilter/" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/etc/easytier/" >> $(PKG_BUILD_DIR)/lucky.keep
	echo "/etc/AdGuardHome/" >> $(PKG_BUILD_DIR)/lucky.keep
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/lucky
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_DIR) $(1)/lib/upgrade/keep.d/
	
	$(INSTALL_BIN) ./files/lucky.init $(1)/etc/init.d/lucky
	$(INSTALL_CONF) $(CURDIR)/files/luckyuci $(1)/etc/config/lucky
	
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/lucky.keep $(1)/lib/upgrade/keep.d/lucky
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
