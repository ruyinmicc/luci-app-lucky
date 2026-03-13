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
		LUCKY_ARCH:=armv6
	else
		LUCKY_ARCH:=armv7
	endif
endif
ifeq ($(BOARD),bcm53xx)
	LUCKY_ARCH:=armv6
ifeq ($(word 2,$(subst +,$(space),$(call qstrip,$(CONFIG_CPU_TYPE)))),)
	LUCKY_ARCH:=armv5
endif
endif
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
	# 创建构建目录
	mkdir -p $(PKG_BUILD_DIR)
	# 不再下载二进制文件，只准备需要的文件
	# 如果需要从files目录复制某些文件，可以在这里添加
endef



define Package/$(PKG_NAME)/conffiles
/etc/config/lucky
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	# $(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/config/
	# $(INSTALL_BIN) $(PKG_BUILD_DIR)/lucky $(1)/usr/bin/lucky
	$(INSTALL_BIN) ./files/lucky.init $(1)/etc/init.d/lucky
	$(INSTALL_CONF) $(CURDIR)/files/luckyuci $(1)/etc/config/lucky
endef



$(eval $(call BuildPackage,$(PKG_NAME)))
