#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libpam
PKG_VERSION:=1.1.4
PKG_RELEASE:=1

PKG_SOURCE:=Linux-PAM-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://pkgs.fedoraproject.org/repo/pkgs/pam/Linux-PAM-1.1.4.tar.bz2/e9af5fb27bb22edb55d077e2888b3ebc/
PKG_MD5SUM:=e9af5fb27bb22edb55d077e2888b3ebc
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

PKG_BUILD_DIR:=$(BUILD_DIR)/Linux-PAM-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/libpam
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=free implementation of the following DCE-RFC from Sunsoft.
  URL:=http://www.kernel.org/pub/linux/libs/pam
  DEPENDS:=+libtirpc
endef

define Package/libpam/description
	Linux-PAM is a free implementation of the following DCE-RFC from Sunsoft. 

endef

TARGET_CFLAGS += $(FPIC)

define Build/Configure
	(cd $(PKG_BUILD_DIR); autoreconf -v -f --install || exit 1)
	$(call Build/Configure/Default, \
		--libdir=$(TOOLCHAIN_DIR)/lib \
		--enable-db=no \
		--enable-shared \
		--enable-static \
		--enable-pamlocking \
		--disable-prelude \
		--disable-lckpwdf \
		--disable-selinux \
		--disable-nls \
		--disable-rpath \
	)
endef



define Build/InstallDev
	$(INSTALL_DIR) $(1)/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/include/security
	$(CP) $(PKG_INSTALL_DIR)/$(TOOLCHAIN_DIR)/lib/* $(1)/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/security/* $(1)/usr/include/security
endef

define Package/libpam/conffiles
/etc/security
/etc/pam.conf
endef

define Package/libpam/install
	$(INSTALL_DIR) $(1)/lib
	$(INSTALL_DIR) $(1)/lib/security
	$(INSTALL_DIR) $(1)/lib/security/pam_filter
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/lib
	$(CP) $(PKG_INSTALL_DIR)/$(TOOLCHAIN_DIR)/lib/*.so* $(1)/lib/
	$(CP) $(PKG_INSTALL_DIR)/$(TOOLCHAIN_DIR)/lib/security/*.so* $(1)/lib/security
	$(CP) $(PKG_INSTALL_DIR)/$(TOOLCHAIN_DIR)/lib/security/pam_filter/* $(1)/lib/security/pam_filter
	$(CP) $(PKG_INSTALL_DIR)/etc/* $(1)/etc/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/* $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,libpam))
