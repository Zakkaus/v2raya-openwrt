# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021-2023 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=v2raya-core
PKG_VERSION:=2.5.5
PKG_RELEASE:=1

PKG_SOURCE:=v2rayA-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/v2rayA/v2rayA/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=1c827bbafffeef1c43aea153877c184f40af5dc6871646bf85215f0b0086570b
PKG_BUILD_DIR:=$(BUILD_DIR)/v2rayA-$(PKG_VERSION)/core

PKG_LICENSE:=MPL-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/v2rayA/v2raya-core
GO_PKG_BUILD_PKG:=github.com/v2rayA/v2raya-core/main
GO_PKG_LDFLAGS_X:= \
	main.Version=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1)/.. $(TAR_OPTIONS)

GO_PKG_TARGET_VARS:=$(filter-out CGO_ENABLED=%,$(GO_PKG_TARGET_VARS)) CGO_ENABLED=0
GO_PKG_DEFAULT_LDFLAGS:=$(filter-out -linkmode external,$(GO_PKG_DEFAULT_LDFLAGS))
GO_PKG_BUILD_VARS:=$(filter-out GOTOOLCHAIN=%,$(GO_PKG_BUILD_VARS)) GOTOOLCHAIN=go1.26.0+auto

define Package/v2raya-core
  TITLE:=The Xray-based core of v2rayA
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
  URL:=https://github.com/v2rayA/v2rayA
endef

define Package/v2raya-core/description
  v2raya_core is the proxy core v2rayA starts: xray-core with v2rayA's
  DNS module, load balancing and TUN. v2rayA needs the core of exactly
  its own version.
endef

define Package/v2raya-core/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/main $(1)/usr/bin/v2raya_core
endef

$(eval $(call GoBinPackage,v2raya-core))
$(eval $(call BuildPackage,v2raya-core))
