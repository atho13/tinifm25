include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-tinyfm
PKG_VERSION:=2.5.3
PKG_RELEASE:=7

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Frdmx <https://github.com>

# Dependensi sistem dan PHP8
LUCI_TITLE:=LuCI support for TinyFM
LUCI_DEPENDS:=+php8 +php8-cgi +php8-fastcgi +php8-fpm \
    +php8-mod-session +php8-mod-ctype +php8-mod-fileinfo \
    +php8-mod-zip +php8-mod-iconv +php8-mod-mbstring \
    +coreutils-stat +zoneinfo-asia
LUCI_PKGARCH:=all

# WAJIB: Sertakan luci.mk di sini
include $(TOPDIR)/feeds/luci/luci.mk

define Package/$(PKG_NAME)/description
 LuCI interface for TinyFM file manager with auto-configured PHP8 and symlinks.
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/www/tinyfm
	# Salin file dari folder root di repo ke sistem target
	if [ -d ./root ]; then \
		$(CP) ./root/* $(1)/; \
	fi
endef

# Bagian postinst yang Anda tulis
define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
    mkdir -p /www/tinyfm
    ln -sf / /www/tinyfm/rootfs
    ln -sf /etc/openclash /www/tinyfm/openclash

    PHP_INI=$(ls /etc/php.ini /etc/php8/php.ini 2>/dev/null | head -n1)
    if [ -f "$$PHP_INI" ]; then
        sed -i 's/^memory_limit.*/memory_limit = 512M/' "$$PHP_INI"
        sed -i 's/^upload_max_filesize.*/upload_max_filesize = 1024M/' "$$PHP_INI"
        sed -i 's/^post_max_size.*/post_max_size = 1024M/' "$$PHP_INI"
        sed -i 's/^max_execution_time.*/max_execution_time = 300/' "$$PHP_INI"
    fi

    uci set uhttpd.main.index_page='index.php'
    uci set uhttpd.main.interpreter='.php=/usr/bin/php-cgi'
    uci commit uhttpd

    [ -x /etc/init.d/php8-fpm ] && /etc/init.d/php8-fpm restart
    [ -x /etc/init.d/uhttpd ] && /etc/init.d/uhttpd restart
fi
exit 0
endef

# Bagian prerm yang Anda tulis
define Package/$(PKG_NAME)/prerm
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
    [ -L "/www/tinyfm/rootfs" ] && rm -f "/www/tinyfm/rootfs"
    [ -L "/www/tinyfm/openclash" ] && rm -f "/www/tinyfm/openclash"

    PHP_INI=$(ls /etc/php.ini /etc/php8/php.ini 2>/dev/null | head -n1)
    if [ -f "$$PHP_INI" ]; then
        sed -i 's/^memory_limit.*/memory_limit = 128M/' "$$PHP_INI"
    fi

    uci del uhttpd.main.interpreter
    uci commit uhttpd

    [ -x /etc/init.d/uhttpd ] && /etc/init.d/uhttpd restart
fi
exit 0
endef

# JANGAN panggil BuildPackage lagi karena sudah dipanggil oleh luci.mk di atas
