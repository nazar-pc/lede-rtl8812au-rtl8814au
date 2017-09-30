include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=rtl8814au
PKG_VERSION=2017-09-30-$(PKG_SOURCE_VERSION)
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nazar-pc/rtl8814AU.git
PKG_SOURCE_VERSION:=7b129626b334c8df1d1e87643d9b04bd33f86af4

include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8814au
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL8814AU support
  DEPENDS:= @USB_SUPPORT +kmod-usb-core +kmod-mac80211
  FILES:= $(PKG_BUILD_DIR)/8814au.ko
#  AUTOLOAD:=$(call AutoLoad,rtl8814au)
endef

define Build/Compile
	$(MAKE) $(KERNEL_MAKEOPTS) M=$(PKG_BUILD_DIR) \
		USER_EXTRA_CFLAGS="-D_LINUX_BYTEORDER_SWAB_H -DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT" \
		CONFIG_RTL8814A=y CONFIG_RTL8814AU=m \
		modules
endef

$(eval $(call KernelPackage,rtl8814au))
