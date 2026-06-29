# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021-2026 Your Name <your.email@example.com>
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mihomo
PKG_VERSION:=1.19.27
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/MetaCubeX/mihomo/archive/refs/tags/
PKG_SOURCE_SUBDIR:=mihomo-v$(PKG_VERSION)
PKG_HASH:=5d90ebe9057b2d996ba4bae237f4a277101d72a923117b4ae0dd97d0c7dc584f

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Your Name <your.email@example.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

# 定义 Go 包路径（mihomo 的主包在根目录）
# GO_PKG:=github.com/MetaCubeX/mihomo

# 如果需要注入版本信息
GO_PKG_LDFLAGS_X:=main.Version=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/mihomo
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Proxy
  TITLE:=Mihomo Proxy Client
  URL:=https://github.com/MetaCubeX/mihomo
  DEPENDS:=$(GO_ARCH_DEPENDS) +libc +libgcc
endef

define Package/mihomo/description
  Mihomo is a simple and fast proxy client.
  This package compiles mihomo from source.
endef

# 如果需要在安装时添加配置文件或启动脚本，可在此定义
# define Package/mihomo/conffiles
# /etc/config/mihomo
# endef

define Package/mihomo/install
	$(call GoPackage/Package/Install/Bin,$(1))
endef

$(eval $(call GoBinPackage,mihomo))
$(eval $(call BuildPackage,mihomo))
