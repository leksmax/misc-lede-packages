include $(TOPDIR)/rules.mk

PKG_NAME:=phytool
PKG_RELEASE:=1

PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/wkz/phytool.git
PKG_SOURCE_DATE:=2017-09-12
PKG_SOURCE_VERSION:=8882328c08ba2efb13c049812098f1d0cb8adf0c
PKG_MIRROR_HASH:=4e87ab5c4bcbff9f1e98e8d54107001396f9bae889d5252bc17b4505eef0be90

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Christian Lamparter <chunkeey@googlemail.com>

include $(INCLUDE_DIR)/package.mk

define Package/phytool
  SECTION:=net
  CATEGORY:=Network
  TITLE:=phytool Linux MDIO register access
  URL:=https://github.com/wkz/phytool.git
endef

define Package/phytool/description
   Linux MDIO register access
endef

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/phytool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/phytool $(1)/usr/bin/
endef

$(eval $(call BuildPackage,phytool))
