#
# Copyright (C) 2011-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mbedtls
PKG_VERSION:=2.4.0
PKG_RELEASE:=2
PKG_USE_MIPS16:=0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-gpl.tgz
PKG_SOURCE_URL:=https://tls.mbed.org/download/
PKG_HASH:=80eff0e0028f969355d6e34ffdd3dbf4eb2a9367b07ff2f3f70e6d75beee9e3f

PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2.0+

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/mbedtls/Default
  SUBMENU:=SSL
  TITLE:=Embedded SSL
  URL:=https://tls.mbed.org
endef

define Package/mbedtls/Default/description
The aim of the mbedtls project is to provide a quality, open-source
cryptographic library written in C and targeted at embedded systems.
endef

define Package/libmbedtls
$(call Package/mbedtls/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= (library)
  ABI_VERSION:=$(PKG_VERSION)-$(PKG_RELEASE)
endef

define Package/libmbedtls/description
$(call Package/mbedtls/Default/description)
This package contains the mbedtls library.
endef

PKG_INSTALL:=1

CMAKE_OPTIONS += \
	-DCMAKE_BUILD_TYPE:String="Release" \
	-DUSE_SHARED_MBEDTLS_LIBRARY:Bool=ON \
	-DENABLE_TESTING:Bool=OFF \
	-DENABLE_PROGRAMS:Bool=OFF \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/mbedtls $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so* $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.a $(1)/opt/lib/
endef

define Package/libmbedtls/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/lib*.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libmbedtls))
