#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=alpine
PKG_VERSION:=2.10
PKG_RELEASE:=1

PKG_SOURCE_URL:=http://patches.freeiz.com/alpine/patches/alpine-2.10/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).clean.tar.lzma
PKG_MD5SUM:=727a6eaa577857b98ea74fac6ea42a25

PKG_CAT:=lzcat
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/alpine
  SECTION:=mail
  CATEGORY:=Mail
  DEPENDS:=+libopenssl +libncurses +libpthread
  TITLE:=Alternatively Licensed Program for Internet News and Email
  URL:=http://www.washington.edu/alpine
endef

define Package/alpine/description
 Alpine (Alternatively Licenced Program for Internet News and Email) is a
 free software email client developed at the University of Washington.
 It is suitable for both the inexperienced email user as well as for
 the most demanding power user.
endef

CONFIGURE_ARGS += \
	--with-ssl-include-dir=$(STAGING_DIR)/usr/include/openssl/. \
	--without-tcl \
	--without-ldap \
	--without-krb5 \
	--with-system-pinerc=/etc/pine.conf \
	--with-system-fixed-pinerc=/etc/pine.conf.fixed \
	--disable-debug \
	--disable-mouse \
	--with-c-client-target=slx \

ifeq ($(CONFIG_IPV6),y)
  DISABLE_IPV6:=
else
  DISABLE_IPV6:=--without-ipv6
endif

define Build/Compile
	( cd $(PKG_BUILD_DIR)/pith ; \
		$(HOSTCC) help_h_gen.c -c -o help_h_gen.o ; \
		$(HOSTCC) help_h_gen.o -o help_h_gen ; \
		$(HOSTCC) help_c_gen.c -c -o help_c_gen.o ; \
		$(HOSTCC) help_c_gen.o -o help_c_gen ; \
	)
	$(call Build/Compile/Default)
endef

define Package/alpine/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/alpine $(1)/usr/bin/
endef

$(eval $(call BuildPackage,alpine))
