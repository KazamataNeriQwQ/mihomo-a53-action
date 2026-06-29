# SPDX-License-Identifier: GPL-2.0-or-later

include $(TOPDIR)/rules.mk

PKG_NAME:=mihomo
PKG_VERSION:=1.19.27
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/MetaCubeX/mihomo.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)   # 解压后的目录名
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz   # 只是个名字，实际不下载
PKG_HASH:=skip

PKG_BUILD_DEPENDS:=golang/host
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Your Name <your.email@example.com>

include $(INCLUDE_DIR)/package.mk

define Package/mihomo
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Proxy
  TITLE:=Mihomo Proxy Client
  URL:=https://github.com/MetaCubeX/mihomo
  DEPENDS:=+libc +libgcc
endef

define Package/mihomo/description
  Mihomo is a simple and fast proxy client.
  This package compiles the mihomo binary from source.
endef

define Build/Compile
	( \
		cd $(PKG_BUILD_DIR); \
		CGO_ENABLED=1 \
		GOOS=linux \
		GOARCH=$(ARCH) \
		$(if $(CONFIG_arm),GOARM=7,) \
		go build -v \
		-buildvcs=false \
		-tags with_gvisor \
		-trimpath \
		-ldflags="-w -s -buildid=" \
		-o $(PKG_NAME) . \
	)
endef

define Package/mihomo/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mihomo))
