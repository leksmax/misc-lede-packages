include $(TOPDIR)/rules.mk

PKG_NAME:=softoff
PKG_VERSION:=2017-10-04
PKG_RELEASE=1
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Christian Lamparter <chunkeey@googlemail.com>

include $(INCLUDE_DIR)/package.mk

define Package/softoff
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=softoff utility
	DEPENDS:=+hdparm
endef

define Package/softoff/description
  softoff allows embedded devices with out a working poweroff method to become unavailable.
endef

define Build/Compile
        true
endef

define Package/softoff/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) ./files/softoff $(1)/sbin/softoff
endef

$(eval $(call BuildPackage,softoff))
