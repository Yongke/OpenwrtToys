include $(TOPDIR)/rules.mk

PKG_NAME:=jemalloc
PKG_VERSION:=4.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.canonware.com/download/jemalloc/
PKG_MD5SUM:=

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libjemalloc
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=General purpose malloc(3) implementation
  DEPENDS:=+libpthread
  URL:=http://www.canonware.com/
endef

define Package/libjemalloc/description
jemalloc is a general purpose malloc(3) implementation that emphasizes
fragmentation avoidance and scalable concurrency support.  jemalloc first came
into use as the FreeBSD libc allocator in 2005, and since then it has found its
way into numerous applications that rely on its predictable behavior.  In 2010
jemalloc development efforts broadened to include developer support features
such as heap profiling, Valgrind integration, and extensive monitoring/tuning
hooks.  Modern jemalloc releases continue to be integrated back into FreeBSD,
and therefore versatility remains critical.  Ongoing development efforts trend
toward making jemalloc among the best allocators for a broad range of demanding
applications, and eliminating/mitigating weaknesses that have practical
repercussions for real world applications.
endef

TARGET_CFLAGS += $(FPIC)
define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/jemalloc/jemalloc.h $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/libjemalloc.{a,so*} $(1)/usr/lib/
endef

define Package/libjemalloc/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/libjemalloc.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libjemalloc))
