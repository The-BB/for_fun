# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PECL_NAME:=timezonedb
PECL_LONGNAME:=Timezone Database

PKG_VERSION:=2021.1
PKG_RELEASE:=1

PKG_NAME:=php7-pecl-$(PECL_NAME)
PKG_SOURCE:=$(PECL_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=https://pecl.php.net/get
PKG_HASH:=9fd473fc76e01a2ffcd087283d20e4ec14067b29a8336ac4acf9c564abbeaa55

PKG_BUILD_DIR:=$(BUILD_DIR)/pecl-php7/$(PECL_NAME)-$(PKG_VERSION)

PKG_LICENSE:=PHP-3.01

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/lang/php7/pecl.mk

CONFIGURE_ARGS += \
	--enable-timezonedb

$(eval $(call PHP7PECLPackage,$(PECL_NAME),$(PECL_LONGNAME),,20))
$(eval $(call BuildPackage,$(PKG_NAME)))
