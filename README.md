Required dependencies
---
- copy and paste in OpenWrt terminal
- openwrt 24.10
```shell
opkg update && opkg install php8 php8-cgi php8-fastcgi php8-fpm php8-mod-session php8-mod-ctype php8-mod-fileinfo php8-mod-zip php8-mod-iconv php8-mod-mbstring coreutils-stat zoneinfo-asia
```
- openwrt 25.12
```shell
apk update && apk add php8 php8-cgi php8-fastcgi php8-fpm php8-mod-session php8-mod-ctype php8-mod-fileinfo php8-mod-zip php8-mod-iconv php8-mod-mbstring coreutils-stat zoneinfo-asia
```
