#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=owntone
PKG_VERSION:=28.8
PKG_RELEASE:=1
PKG_REV:=85929dcaa87c71da52e589f9ad049afa41f9922b

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/owntone/owntone-server.git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf
PKG_BUILD_FLAGS:=no-mips16
PKG_INSTALL:=1

PKG_MAINTAINER:=Espen Jürgensen <espenjurgensen+openwrt@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/owntone
SECTION:=sound
CATEGORY:=Sound
TITLE:=iTunes (DAAP) server for Apple Remote and AirPlay
URL:=https://github.com/owntone/owntone-server
DEPENDS:=+libgpg-error +libgcrypt +libgdbm +zlib +libexpat +libunistring \
	+libevent2 +libdaemon +libantlr3c +confuse +alsa-lib +libffmpeg-full \
	+mxml +libavahi-client +sqlite3-cli +libplist +libcurl +libjson-c \
	+libprotobuf-c +libgnutls +libsodium +libwebsockets $(ICONV_DEPENDS) \
	+libevent2-pthreads +libuuid +librt +libpthread
endef

define Package/owntone/description
  OwnTone is a Linux/FreeBSD DAAP (iTunes), MPD (Music Player Daemon) and
  RSP (Roku) media server. It has support for AirPlay speakers, Chromecast,
  Apple Remote (and compatibles), MPD clients, Spotify, internet radio and
  LastFM. It does not support AirPlay/Chromecast video.
endef

define Package/owntone/conffiles
/etc/owntone.conf
endef

CONFIGURE_ARGS += \
	--enable-chromecast \
	--disable-install_systemd \
	--disable-install_conf_file \
	--disable-install_user \
	--with-alsa \
	--without-pulseaudio

TARGET_CFLAGS += $(FPIC)

define Package/owntone/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/owntone $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/owntone.conf $(1)/etc/owntone.conf
	$(INSTALL_DIR) $(1)/usr/lib/owntone
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/owntone/* $(1)/usr/lib/owntone/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/owntone.init $(1)/etc/init.d/owntone
	$(INSTALL_DIR) $(1)/usr/share/owntone
	$(CP) $(PKG_INSTALL_DIR)/usr/share/owntone/htdocs $(1)/usr/share/owntone
endef

$(eval $(call BuildPackage,owntone))
