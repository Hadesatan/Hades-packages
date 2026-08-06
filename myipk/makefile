include $(TOPDIR)/rules.mk

PKG_NAME:=myipk
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=local
PKG_SOURCE:=

include $(INCLUDE_DIR)/package.mk

IPK_LIST := myipk/app1.ipk myipk/app2.ipk myipk/app3.ipk

define Build/Prepare
    mkdir -p $(PKG_BUILD_DIR)/rootfs
    for ipk in $(IPK_LIST); do \
        tmp=$$(mktemp -d); \
        cd $$tmp; \
        ar x $$ipk data.tar.gz; \
        tar -xzf data.tar.gz -C $(PKG_BUILD_DIR)/rootfs; \
        cd -; \
        rm -rf $$tmp; \
    done
endef

# 空编译阶段
define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
    # 复制所有解包文件到固件根目录
    cp -r $(PKG_BUILD_DIR)/rootfs/* $(1)/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
