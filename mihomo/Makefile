include $(TOPDIR)/rules.mk

PKG_NAME:=mihomo
PKG_VERSION:=1.19.27
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/MetaCubeX/mihomo/archive/refs/tags/
PKG_SOURCE_SUBDIR:=mihomo-v$(PKG_VERSION)
PKG_HASH:=5d90ebe9057b2d996ba4bae237f4a277101d72a923117b4ae0dd97d0c7dc584f

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
endef

define Build/Compile
	( \
		cd $(PKG_BUILD_DIR); \
		case "$(ARCH)" in \
			aarch64) export GOARCH=arm64;; \
			x86_64)  export GOARCH=amd64;; \
			arm)     export GOARCH=arm; export GOARM=7;; \
			mips)    export GOARCH=mips;; \
			mipsel)  export GOARCH=mipsle;; \
			riscv64) export GOARCH=riscv64;; \
			*)       export GOARCH=$(ARCH);; \
		esac; \
		export CGO_ENABLED=1; \
		export GOOS=linux; \
		go build -v \
		-buildvcs=false \
		-tags with_gvisor \
		-trimpath \
		-ldflags="-w -s -buildid= -linkmode=external" \
		-o $(PKG_NAME) . \
	)
endef

define Package/mihomo/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mihomo))
