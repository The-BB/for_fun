# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=dnsproxy
PKG_VERSION:=v0.36.0
PKG_RELEASE:=1

PKG_GOGET:=github.com/AdguardTeam/dnsproxy

GOPKG_SOURCE=GO_$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.bz2

#!!! uncomment PKG_SOURCE to download fixed version
#PKG_SOURCE=$(GOPKG_SOURCE)
PKG_COMMIT=94393538312a58e287bc9460b469f2b336b355da
PKG_HASH:=skip

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/golang.mk

ifeq ($(BUILD_VARIANT),nohf)
GOARM:=GOARM=5
endif

define Package/dnsproxy/Default
	$(call Package/gopackage/Default)
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=IP Addresses and Names
	TITLE:=Simple DNS proxy with DoH, DoT, DoQ and DNSCrypt support
	URL:=https://github.com/AdguardTeam/dnsproxy
endef

define Package/dnsproxy
	$(call Package/dnsproxy/Default)
	VARIANT:=hf
endef

define Package/dnsproxy_nohf
	$(call Package/dnsproxy/Default)
	VARIANT:=nohf
	DEPENDS+=@(TARGET_armv7_2_6||TARGET_armv7_3_2)
endef

define Package/dnsproxy/description
    A simple DNS proxy server that supports all existing DNS
  protocols including DNS-over-TLS, DNS-over-HTTPS, DNSCrypt,
  and DNS-over-QUIC. Moreover, it can work as a DNS-over-HTTPS,
  DNS-over-TLS or DNS-over-QUIC server.
endef

Package/dnsproxy_nohf/description=$(Package/dnsproxy/description)

define Build/Compile
	( cd $(PKG_BUILD_DIR)/src/$(PKG_GOGET); \
		CGO_ENABLED=0 \
		GOOS=linux \
		GOARCH=$(GOARCH) \
		$(GOARM) \
		$(GOROOT)/bin/go build . ; \
	)
endef

define Package/dnsproxy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/$(PKG_GOGET)/dnsproxy $(1)/opt/bin
endef

Package/dnsproxy_nohf/install=$(Package/dnsproxy/install)

$(eval $(call BuildPackage,dnsproxy))
$(eval $(call BuildPackage,dnsproxy_nohf))
