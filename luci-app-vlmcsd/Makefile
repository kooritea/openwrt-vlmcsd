include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-vlmcsd
PKG_VERSION:=1.0.2
PKG_RELEASE:=2

PKG_MAINTAINER:=kooritea <admin@kooritea.moe>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_PARALLEL:=2

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=3. Applications
	TITLE:=LuCI app for openwrt-vlmcsd
	DEPENDS:=+vlmcsd
	PKGARCH:=all
	MAINTAINER:=kooritea
endef

define Package/$(PKG_NAME)/description
	This package contains LuCI configuration pages for openwrt-vlmcsd.
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef


define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
	( . /etc/uci-defaults/luci-app-vlmcsd ) && rm -f /etc/uci-defaults/luci-app-vlmcsd
	rm -f /tmp/luci-indexcache
	sed -i '/srv-host=_vlmcs._tcp.lan/d' /etc/dnsmasq.conf
fi
exit 0
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DIR) $(1)/etc/config

	$(INSTALL_BIN) ./files/luci-app-vlmcsd $(1)/etc/uci-defaults/luci-app-vlmcsd
	$(INSTALL_CONF) ./files/vlmcsd.config $(1)/etc/config/vlmcsd
	$(INSTALL_DATA) ./files/luci/i18n/vlmcsd.zh-cn.lmo $(1)/usr/lib/lua/luci/i18n/vlmcsd.zh-cn.lmo
	$(INSTALL_DATA) ./files/luci/model/vlmcsd.lua $(1)/usr/lib/lua/luci/model/cbi/vlmcsd.lua
	$(INSTALL_DATA) ./files/luci/controller/vlmcsd.lua $(1)/usr/lib/lua/luci/controller/vlmcsd.lua
endef

$(eval $(call BuildPackage,$(PKG_NAME)))