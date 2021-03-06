# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-netifaces
PKG_VERSION:=0.10.7
PKG_RELEASE:=1

PKG_SOURCE:=netifaces-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/81/39/4e9a026265ba944ddf1fea176dbb29e0fe50c43717ba4fcf3646d099fe38
PKG_HASH:=bd590fcb75421537d4149825e1e63cca225fd47dad861710c46bd1cb329d8cbd

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-$(PKG_NAME)-$(PKG_VERSION)

OW_VER:=$(shell git --git-dir=$(TOPDIR)/.git describe --abbrev=0 --always --tag)
ifneq ($(filter reboot v19.07% v18.06%, $(OW_VER)),)
	IS_HEAD:=y
endif

include $(INCLUDE_DIR)/package.mk

ifeq ($(IS_HEAD),y)
	include ../python-package.mk
	include ../python3-package.mk
else
	$(call include_mk, python-package.mk)
	$(call include_mk, python3-package.mk)
endif

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

define Package/python-netifaces/Default
	SECTION:=lang
	CATEGORY:=Languages
	SUBMENU:=Python
	URL:=https://bitbucket.org/al45tair/netifaces
	MAINTAINER:=Alastair Houghton <alastair@alastairs-place.net>
endef

define Package/python-netifaces
	$(call Package/python-netifaces/Default)
	TITLE:=python-netifaces
	DEPENDS:=+PACKAGE_python-netifaces:python-light
	VARIANT:=python
endef

define Package/python3-netifaces
	$(call Package/python-netifaces/Default)
	TITLE:=python3-netifaces
	DEPENDS:=+PACKAGE_python3-netifaces:python3-light
	VARIANT:=python3
endef

define Package/python-netifaces/description
	Portable network interface information.
endef

define Package/python3-netifaces/description
	$(call Package/python-netifaces/description)
	.
	(Variant for Python3)
endef

$(eval $(call PyPackage,python-netifaces))
$(eval $(call BuildPackage,python-netifaces))
$(eval $(call Py3Package,python3-netifaces))
$(eval $(call BuildPackage,python3-netifaces))
