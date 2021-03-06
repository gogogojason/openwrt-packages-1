include $(TOPDIR)/rules.mk

PKG_NAME:=shadowsocksr-libev
PKG_VERSION:=2.5.6
PKG_RELEASE:=6

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/shadowsocksrr/shadowsocksr-libev
PKG_MIRROR_HASH:=834ce598f940fb9db2bf4c0d1f8cfa883df27c1c8553dbcb306d6f32ae13c317
PKG_SOURCE_VERSION:=d63ff863800a5645aca4309d5dd5962bd1e95543
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/shadowsocksr-libev/Default
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=Lightweight Secured Socks5 Proxy
	URL:=https://github.com/shadowsocksrr/shadowsocksr-libev
	DEPENDS:=+libev +libsodium +libopenssl +libpthread +libpcre +libudns +zlib
	PROVIDES:=shadowsocksr-libev
endef

Package/shadowsocksr-libev-server = $(Package/shadowsocksr-libev/Default)
Package/shadowsocksr-libev-alt = $(Package/shadowsocksr-libev/Default)
Package/shadowsocksr-libev-ssr-local = $(Package/shadowsocksr-libev/Default)

CONFIGURE_ARGS += --disable-documentation --disable-ssp --disable-assert \
	--enable-system-shared-lib

TARGET_CFLAGS += -flto
TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

define Package/shadowsocksr-libev-alt/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ss-redir $(1)/usr/bin/ssr-redir
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/ss-check $(1)/usr/bin/ssr-check
endef

define Package/shadowsocksr-libev-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/server/ss-server $(1)/usr/bin/ssr-server
endef

define Package/shadowsocksr-libev-ssr-local/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ss-local $(1)/usr/bin/ssr-local
	$(LN) ssr-local $(1)/usr/bin/ssr-tunnel
endef

$(eval $(call BuildPackage,shadowsocksr-libev-alt))
$(eval $(call BuildPackage,shadowsocksr-libev-server))
$(eval $(call BuildPackage,shadowsocksr-libev-ssr-local))
