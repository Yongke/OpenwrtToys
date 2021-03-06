include $(TOPDIR)/rules.mk

PKG_NAME:=redis
PKG_VERSION:=2.8.13
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://download.redis.io/releases/
PKG_MD5SUM:=

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

MAKE_FLAGS+= \
	MALLOC="jemalloc" \
	PREFIX="$(PKG_INSTALL_DIR)/usr"

define Package/redis
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Advanced key-value cache and store
  DEPENDS:=+libpthread
  URL:=http://redis.io
endef

define Package/redis/description
	Redis is an open source, BSD licensed, advanced key-value cache and store.
	It is often referred to as a data structure server since keys can contain
	strings, hashes, lists, sets, sorted sets, bitmaps and hyperloglogs.
endef

define Package/redis/conffiles
/etc/redis.conf
endef

define Build/Compile
	sed -e 's#^\(REAL_CFLAGS.* \)$$$$(ARCH)#\1#g' -i $(PKG_BUILD_DIR)/deps/hiredis/Makefile
	$(call Build/Compile/Default, PLAT=linux GNU_TARGET_NAME=$(GNU_TARGET_NAME))
endef

define Package/redis/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/$(PKG_NAME)-server $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/redis.init $(1)/etc/init.d/redis
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) ./files/redis.conf $(1)/etc
endef

$(eval $(call BuildPackage,redis))
