include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-tinyfm
PKG_VERSION:=2.5.3
PKG_RELEASE:=6

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Yogxx <https://github.com/Yogxx/tinyfm>

LUCI_TITLE:=LuCI support for TinyFM
LUCI_DEPENDS:=
LUCI_PKGARCH:=all

include $(TOPDIR)/feeds/luci/luci.mk


define Package/$(PKG_NAME)/description
 LuCI interface for TinyFM file manager.
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
    echo "Installing PHP dependencies..."
    if command -v apk > /dev/null 2>&1; then
        apk add php8 php8-cgi php8-fastcgi php8-fpm \
            php8-mod-session php8-mod-ctype php8-mod-fileinfo \
            php8-mod-zip php8-mod-iconv php8-mod-mbstring \
            coreutils-stat zoneinfo-asia
    elif command -v opkg > /dev/null 2>&1; then
        opkg update
        opkg install php8 php8-cgi php8-fastcgi php8-fpm \
            php8-mod-session php8-mod-ctype php8-mod-fileinfo \
            php8-mod-zip php8-mod-iconv php8-mod-mbstring \
            coreutils-stat zoneinfo-asia
    else
        echo "ERROR: No package manager found (apk/opkg)"
        exit 1
    fi
fi
exit 0
endef

define Package/$(PKG_NAME)/install

	# Install root files (jika ada)
	if [ -d ./root ]; then \
		$(CP) ./root/* $(1)/; \
	fi

endef


$(eval $(call BuildPackage,$(PKG_NAME)))
