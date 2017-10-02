include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=rtl8814au
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nazar-pc/RTL8814AU.git
PKG_SOURCE_DATE:=2017-10-02
PKG_SOURCE_VERSION:=ccc5e12354a5d449ce5a060d8a71497c2eede57a

include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8814au
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL8814AU support
  DEPENDS:= +kmod-usb-core +kmod-cfg80211 @USB_SUPPORT +@DRIVER_11N_SUPPORT +@DRIVER_11AC_SUPPORT
  FILES:= $(PKG_BUILD_DIR)/rtl8814au.ko
  AUTOLOAD:=$(call AutoLoad,50,cfg80211 rtl8814au)
endef

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-include backport/backport.h

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		CONFIG_RTL8814AU=m \
		modules
endef

define KernelPackage/rtl8814au/install
	$(INSTALL_DIR) $(1)/lib/firmware
	$(INSTALL_DIR) $(1)/lib/firmware/rtlwifi
	$(CP) $(PKG_BUILD_DIR)/firmware/rtl8814aufw.bin $(1)/lib/firmware/rtlwifi/
endef

$(eval $(call KernelPackage,rtl8814au))
