#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=grilo-plugins
PKG_VERSION:=0.2.16
PKG_RELEASE:=1

PKG_MAINTAINER:=W. Michael Petullo <mike@flyn.org>

PKG_LICENSE:=LGPLv2.1
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://download.gnome.org/sources/grilo-plugins/0.2/
PKG_MD5SUM:=62ecaad877b485a950259eef1ef38c18

PKG_BUILD_DEPENDS:=glib2 grilo

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/grilo-plugins/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=grilo-plugins
  URL:=https://wiki.gnome.org/Projects/Grilo
endef

define Package/grilo-plugins
  $(call Package/grilo-plugins/Default)
  MENU:=1
  DEPENDS:=+grilo $(ICONV_DEPENDS) $(INTL_DEPENDS)
  TITLE:=Plugins for the Grilo framework
endef

define Package/grilo/decription
  Grilo is a framework that provides access to different sources of
  multimedia content, using a pluggable system. This package contains 
  plugins to get information from a number of sources.
endef

CONFIGURE_ARGS += \
        --enable-static \
        --without-libiconv-prefix \
        --without-libintl-prefix \
        --without-x \

define Package/grilo-plugins/install
	$(INSTALL_DIR) $(1)/usr/lib/grilo-0.2
endef

define BuildPlugin
  define Package/grilo-plugins-$(1)
    $(call Package/grilo-plugins/Default)
    DEPENDS:=grilo-plugins
    ifneq ($(4),)
      DEPENDS+= $(4)
    endif
    TITLE:=$(2) plugin
  endef

  define Package/grilo-plugins-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/grilo-0.2
	for p in $(3); do \
		$(CP) $(PKG_INSTALL_DIR)/usr/lib/grilo-0.2/libgrl$$$$$$$${p}.so $$(1)/usr/lib/grilo-0.2; \
		$(CP) $(PKG_INSTALL_DIR)/usr/lib/grilo-0.2/grl-$$$$$$$${p}.xml $$(1)/usr/lib/grilo-0.2; \
	done
  endef

  $$(eval $$(call BuildPackage,grilo-plugins-$(1)))
endef

$(eval $(call BuildPackage,grilo-plugins))

$(eval $(call BuildPlugin,dleyna,DLNA sharing,dleyna,,30))
$(eval $(call BuildPlugin,dmap,DAAP and DPAP sharing,daap dpap,libdmapsharing,30))
$(eval $(call BuildPlugin,gravatar,Gravatar provider,gravatar,,30))
$(eval $(call BuildPlugin,jamendo,Jamendo sharing,jamendo,,30))
$(eval $(call BuildPlugin,lastfm-albumart,Last.FM album art provider,lastfm-albumart,,30))
$(eval $(call BuildPlugin,magnatune,Magnatune sharing,magnatune,,30))
$(eval $(call BuildPlugin,metadata-store,Extra metadata store,metadata-store,,30))
$(eval $(call BuildPlugin,opensubtitles,Openi subtitles provider,opensubtitles,,30))
$(eval $(call BuildPlugin,raitv,Rai.tv sharing,raitv,,30))
$(eval $(call BuildPlugin,shoutcast,SHOUTcast sharing,shoutcast,,30))
