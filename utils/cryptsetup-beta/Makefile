#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cryptsetup-beta
PKG_VERSION:=1.99.0-git
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0+ LGPL-2.1+
PKG_LICENSE_FILES:=COPYING COPYING.LGPL

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.com/cryptsetup/cryptsetup.git
PKG_SOURCE_DATE:=2017-10-04
PKG_SOURCE_VERSION:=30a42bfd8f62633c2b8eb09f2646c70e20cf61f8
PKG_MIRROR_HASH:=cae02ce536464a924f87075eaf723aafc1cd222511cce3b618776333bd0d26bf

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Package/cryptsetup-beta/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Encryption
  TITLE:=Cryptsetup
  DEPENDS:=+libblkid +libuuid +libpopt +lvm2 +libdevmapper +libjson-c +@KERNEL_DIRECT_IO
  URL:=http://code.google.com/p/cryptsetup/
endef

define Package/cryptsetup-beta
$(call Package/cryptsetup-beta/Default)
  DEPENDS+=+libgcrypt
  VARIANT:=gcrypt
endef

define Package/cryptsetup-beta-openssl
$(call Package/cryptsetup-beta/Default)
  TITLE+= (with openssl support)
  DEPENDS+=+libopenssl
  VARIANT:=openssl
endef

define Package/cryptsetup-beta/Default/description
	Cryptsetup-luks
endef

define Package/cryptsetup-beta/description
$(call Package/cryptsetup-beta/Default/description)
linked against libgcrypt
endef


define Package/cryptsetup-beta-openssl/description
$(call Package/cryptsetup-beta/Default/description)
linked against openssl
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); NOCONFIGURE=y ./autogen.sh );
	$(call Build/Configure/Default)
endef

ifeq ($(BUILD_VARIANT),openssl)
CONFIGURE_ARGS+= \
        --with-crypto_backend=openssl
endif

define Package/cryptsetup-beta/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/src/.libs/cryptsetup $(1)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/src/.libs/integritysetup $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/libcryptsetup.so* $(1)/usr/lib
endef

Package/cryptsetup-beta-openssl/install = $(Package/cryptsetup-beta/install)

$(eval $(call BuildPackage,cryptsetup-beta))
$(eval $(call BuildPackage,cryptsetup-beta-openssl))
