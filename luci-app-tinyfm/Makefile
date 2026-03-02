include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-tinyfm
PKG_VERSION:=2.5.3
PKG_RELEASE:=beta

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Yogxx <https://github.com/Yogxx/tinyfm>

LUCI_TITLE:=LuCI support for TinyFM
LUCI_DEPENDS:=+kmod-tun
LUCI_PKGARCH:=all

include $(TOPDIR)/feeds/luci/luci.mk


define Package/$(PKG_NAME)/description
 LuCI interface for TinyFM file manager.
endef


define Package/$(PKG_NAME)/install

	# Install root files (jika ada)
	if [ -d ./root ]; then \
		$(CP) ./root/* $(1)/; \
	fi

endef


$(eval $(call BuildPackage,$(PKG_NAME)))
