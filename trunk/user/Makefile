.EXPORT_ALL_VARIABLES:
.PHONY: all romfs clean

ifndef ROOTDIR
ROOTDIR=..
endif

ifndef ROMFSDIR
ROMFSDIR=$(ROOTDIR)/romfs
endif

UCLINUX_BUILD_USER=1
-include $(LINUX_CONFIG)
include $(PROJECT_CONFIG)
include $(ARCH_CONFIG)

INSTALLDIR = $(ROOTDIR)/romfs

FS_EXT_ENABLED=n
FS_FAT_ENABLED=n
FS_NTFS_ENABLED=n
STORAGE_ENABLED=n
OPENSSH_ENABLED=n
DROPBEAR_ENABLED=n
SAMBA_ENABLED=n
ARIA2_ENABLED=n
SOFTETHERVPN_ENABLE=n
SHADOWSOCKS_ENABLE=n
FRP_ENABLE=n
TROJAN_ENABLE=n

ifneq ($(CONFIG_FIRMWARE_INCLUDE_OPENSSH),y)
ifeq ($(CONFIG_FIRMWARE_INCLUDE_DROPBEAR),y)
DROPBEAR_ENABLED=y
ifeq ($(CONFIG_FIRMWARE_INCLUDE_SFTP),y)
OPENSSH_ENABLED=y
endif
endif
else
OPENSSH_ENABLED=y
endif

ifeq ($(CONFIG_FIRMWARE_INCLUDE_WINS),y)
SAMBA_ENABLED=y
endif

ifdef CONFIG_MMC_BLOCK
STORAGE_ENABLED=y
endif
ifdef CONFIG_BLK_DEV_SD
STORAGE_ENABLED=y
endif

ifeq ($(STORAGE_ENABLED),y)
ifeq ($(CONFIG_FIRMWARE_ENABLE_EXT2),y)
FS_EXT_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_ENABLE_EXT3),y)
FS_EXT_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_ENABLE_EXT4),y)
FS_EXT_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_ENABLE_FAT),y)
FS_FAT_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_ENABLE_EXFAT),y)
FS_FAT_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_NTFS_3G),y)
FS_NTFS_ENABLED=y
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_SMBD),y)
SAMBA_ENABLED=y
endif
endif

ifeq ($(CONFIG_FIRMWARE_INCLUDE_ARIA),y)
ARIA2_ENABLED=y
endif

ifeq ($(CONFIG_FIRMWARE_INCLUDE_REDSOCKS),y)
REDSOCKS_ENABLED=y
endif

ifneq ($(filter y,$(CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_CMD) $(CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_CLIENT) $(CONFIG_FIRMWARE_INCLUDE_SOFTETHERVPN_SERVER)),)
SOFTETHERVPN_ENABLE=y
endif

ifneq ($(filter y,$(CONFIG_FIRMWARE_INCLUDE_SSSERVER) $(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)),)
SHADOWSOCKS_ENABLE=y
endif

ifneq ($(filter y,$(CONFIG_FIRMWARE_INCLUDE_FRPC) $(CONFIG_FIRMWARE_INCLUDE_FRPS)),)
FRP_ENABLE=y
endif

ifneq ($(filter y,$(CONFIG_FIRMWARE_INCLUDE_WING) $(CONFIG_FIRMWARE_INCLUDE_TROJAN)),)
TROJAN_ENABLE=y
endif

dir_y =
dir_n =
dir_  =
dir_y							+= ralinkiappd
dir_y							+= busybox
dir_y							+= iptables
dir_y							+= coremark
ifneq ($(CONFIG_WITHOUT_KERNEL),y)
dir_$(CONFIG_FIRMWARE_INCLUDE_IPSET)			+= ipset
dir_y							+= accel-pptpd
endif
dir_y							+= ebtables
dir_y							+= iproute2
dir_y							+= wireless_tools
dir_y							+= shared
dir_$(STORAGE_ENABLED)			+= libdisk
dir_y							+= nvram
dir_y							+= mtd_write
dir_y							+= networkmap
dir_y							+= httpd
dir_y							+= www
dir_y							+= rc
dir_y							+= jq
dir_$(CONFIG_FIRMWARE_INCLUDE_RTTY)			+= rtty
dir_$(CONFIG_FIRMWARE_INCLUDE_NGINX)			+= nginx
dir_$(CONFIG_FIRMWARE_INCLUDE_ANTFS)			+= antfs
dir_$(CONFIG_FIRMWARE_INCLUDE_NAPT66)			+= napt66
dir_$(CONFIG_FIRMWARE_INCLUDE_SFE)			+= shortcut-fe
dir_y							+= infosvr
dir_y							+= inadyn
dir_y							+= miniupnpd
dir_y							+= dnsmasq
dir_y							+= igmpproxy
ifneq ($(CONFIG_FIRMWARE_INCLUDE_MSD_LITE),y)
dir_y						        += udpxy
endif
dir_y							+= utils
dir_y							+= lanauth
dir_y							+= 802.1x
dir_y							+= wpa_supplicant
dir_y							+= pppd
dir_y							+= pppoe
dir_y                                                 += pppoe-relay
dir_y							+= xl2tpd
dir_$(CONFIG_FIRMWARE_INCLUDE_RPL2TP)			+= rp-l2tp
dir_y							+= lldt
dir_y							+= scripts
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= skipdbv2
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= chinadns-ng
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= lua51
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= microsocks
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= ipt2socks
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)      +=resolveip
dir_$(CONFIG_FIRMWARE_INCLUDE_ADGUARDHOME)     	+= adguardhome
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)	    += dns2tcp
ifeq ($(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS),y)
dir_$(CONFIG_FIRMWARE_INCLUDE_V2RAY)			+= v2ray
dir_$(CONFIG_FIRMWARE_INCLUDE_XRAY)				+= xray
dir_$(CONFIG_FIRMWARE_INCLUDE_TROJAN)			+= trojan
endif
#dir_$(CONFIG_FIRMWARE_INCLUDE_SSOBFS)			+= simple-obfs
dir_$(CONFIG_FIRMWARE_INCLUDE_ZEROTIER)			+= zerotier
dir_$(CONFIG_FIRMWARE_INCLUDE_WYY)				+= unblockmusic
dir_$(OPENSSH_ENABLED)							+= openssh
dir_$(DROPBEAR_ENABLED)							+= dropbear
dir_$(CONFIG_FIRMWARE_INCLUDE_HTOP)				+= htop
dir_$(CONFIG_FIRMWARE_INCLUDE_NANO)				+= nano
dir_$(CONFIG_FIRMWARE_INCLUDE_OPENVPN)			+= openvpn
dir_$(CONFIG_FIRMWARE_INCLUDE_SSWAN)			+= strongswan
dir_$(CONFIG_FIRMWARE_INCLUDE_XUPNPD)			+= xupnpd
dir_$(CONFIG_FIRMWARE_INCLUDE_TCPDUMP)			+= tcpdump
dir_$(CONFIG_FIRMWARE_INCLUDE_MTR)				+= mtr
dir_$(CONFIG_FIRMWARE_INCLUDE_SOCAT)			+= socat
dir_$(CONFIG_FIRMWARE_INCLUDE_NETCAT)			+= netcat
dir_$(CONFIG_FIRMWARE_INCLUDE_SRELAY)			+= srelay
dir_$(CONFIG_FIRMWARE_INCLUDE_TUNSAFE)			+= tunsafe
ifeq ($(CONFIG_FIRMWARE_INCLUDE_WIREGUARD),y)
dir_y += wireguard
dir_y += wireguard-tools
endif
ifeq ($(CONFIG_FIRMWARE_INCLUDE_SMBD36),y)
dir_$(SAMBA_ENABLED)							+= samba36
dir_y											+= wsdd2
else
dir_$(SAMBA_ENABLED)							+= samba3
endif
dir_$(CONFIG_FIRMWARE_INCLUDE_SHADOWSOCKS)		+= chnroute
dir_$(CONFIG_FIRMWARE_INCLUDE_TTYD)				+= ttyd
dir_$(FRP_ENABLE)								+= frp
dir_$(SOFTETHERVPN_ENABLE)						+= softethervpn
dir_$(CONFIG_FIRMWARE_INCLUDE_SCUTCLIENT)		+= scutclient
dir_$(CONFIG_FIRMWARE_INCLUDE_VLMCSD)			+= vlmcsd
dir_$(CONFIG_FIRMWARE_INCLUDE_DNSFORWARDER)		+= dns-forwarder
dir_$(SHADOWSOCKS_ENABLE)						+= shadowsocks
dir_$(CONFIG_FIRMWARE_INCLUDE_LRZSZ)			+= lrzsz
dir_$(CONFIG_FIRMWARE_INCLUDE_GDUT_DRCOM)		+= gdut-drcom
dir_$(CONFIG_FIRMWARE_INCLUDE_DOGCOM)			+= dogcom
dir_$(CONFIG_FIRMWARE_INCLUDE_IPERF3)			+= iperf3
dir_$(CONFIG_FIRMWARE_INCLUDE_MINIEAP)			+= minieap
dir_$(CONFIG_FIRMWARE_INCLUDE_NJIT_CLIENT)		+= njit-client
dir_$(CONFIG_FIRMWARE_INCLUDE_MENTOHUST)		+= mentohust
dir_$(CONFIG_FIRMWARE_INCLUDE_SMARTDNS)			+= smartdns
dir_$(CONFIG_FIRMWARE_INCLUDE_CADDY)			+= caddy
dir_$(CONFIG_FIRMWARE_INCLUDE_xTUN) 			+= xTun
dir_$(CONFIG_FIRMWARE_INCLUDE_WING) 			+= wing
dir_$(CONFIG_FIRMWARE_INCLUDE_WING) 			+= ipt2socks
dir_$(CONFIG_FIRMWARE_INCLUDE_REDSOCKS)			+= redsocks
dir_$(CONFIG_FIRMWARE_INCLUDE_3PROXY)			+= 3proxy
dir_$(CONFIG_FIRMWARE_INCLUDE_MSD_LITE)		        += msd_lite

ifdef CONFIG_BLK_DEV_SD
dir_$(CONFIG_FIRMWARE_INCLUDE_HDPARM)			+= hdparm
endif

ifdef CONFIG_USB_SUPPORT
dir_y											+= p910nd
dir_y											+= usb-modeswitch
dir_y											+= comgt-0.32
dir_y											+= uqmi
dir_$(CONFIG_FIRMWARE_INCLUDE_LPRD)				+= LPRng
dir_$(CONFIG_FIRMWARE_INCLUDE_U2EC)				+= u2ec
dir_$(CONFIG_FIRMWARE_INCLUDE_DUMP1090)			+= dump1090
endif
ifeq ($(STORAGE_ENABLED),y)
dir_$(CONFIG_FIRMWARE_INCLUDE_NFSD)				+= nfs-utils
ifneq (,$(filter y,$(CONFIG_FIRMWARE_INCLUDE_NFSD) $(CONFIG_FIRMWARE_INCLUDE_NFSC)))
dir_y											+= rpcbind
endif
dir_y											+= optware
dir_y											+= util-linux
dir_$(FS_EXT_ENABLED)							+= e2fsprogs
dir_$(FS_FAT_ENABLED)							+= dosfstools
dir_$(FS_NTFS_ENABLED)							+= ntfs-3g
dir_$(CONFIG_FIRMWARE_INCLUDE_PARTED)			+= parted
dir_$(CONFIG_FIRMWARE_INCLUDE_FTPD)				+= vsftpd
dir_$(CONFIG_FIRMWARE_INCLUDE_MINIDLNA)			+= minidlna
dir_$(CONFIG_FIRMWARE_INCLUDE_FIREFLY)			+= firefly
dir_$(CONFIG_FIRMWARE_INCLUDE_TRANSMISSION)		+= transmission
dir_$(ARIA2_ENABLED)							+= aria2
endif

dir_$(CONFIG_FIRMWARE_INCLUDE_KOOLPROXY)		+= koolproxy
dir_$(CONFIG_FIRMWARE_INCLUDE_ADBYBY)			+= adbyby
dir_$(CONFIG_FIRMWARE_INCLUDE_ALIDDNS)			+= aliddns
dir_$(CONFIG_FIRMWARE_INCLUDE_NVPPROXY)			+= nvpproxy
#dir_$(CONFIG_FIRMWARE_INCLUDE_NPC)				+= npc
dir_$(CONFIG_FIRMWARE_INCLUDE_DDNSTO)	        += ddnsto
dir_$(CONFIG_FIRMWARE_INCLUDE_ALDRIVER)	                       += aliyundrive-webdav
dir_$(CONFIG_FIRMWARE_INCLUDE_UUPLUGIN)	                       += uuplugin
dir_$(CONFIG_FIRMWARE_INCLUDE_LUCKY)	                       += lucky
dir_$(CONFIG_FIRMWARE_INCLUDE_WXSEND)	                       += wxsend
dir_$(CONFIG_FIRMWARE_INCLUDE_CLOUDFLARED)	                       += cloudflared
dir_$(CONFIG_FIRMWARE_INCLUDE_VNTS)	                       += vnts
dir_$(CONFIG_FIRMWARE_INCLUDE_VNTCLI)	                       += vntcli
dir_$(CONFIG_FIRMWARE_INCLUDE_NATPIERCE)	                       += natpierce
dir_$(CONFIG_FIRMWARE_INCLUDE_TAILSCALE)	                       += tailscale
dir_$(CONFIG_FIRMWARE_INCLUDE_ALIST)	                       += alist
dir_$(CONFIG_FIRMWARE_INCLUDE_CLOUDFLARE)	                       += cloudflare
dir_$(CONFIG_FIRMWARE_INCLUDE_EASYTIER)	                       += easytier
dir_$(CONFIG_FIRMWARE_INCLUDE_BAFA)	                       += bafa
dir_$(CONFIG_FIRMWARE_INCLUDE_VIRTUALHERE)	                       += virtualhere
dir_$(CONFIG_FIRMWARE_INCLUDE_V2RAYA)	                       += v2raya
dir_$(CONFIG_FIRMWARE_INCLUDE_N2N)	                       += n2n
ifdef CONFIG_MTD_UBI
ifneq ($(STORAGE_ENABLED),y)
dir_y											+= optware
dir_y											+= util-linux
endif
dir_y											+= mtd-utils
endif

all:
	for i in $(dir_y) ; do \
		[ ! -d $$i ] || \
		$(MAKE) -j1 -C $$i || \
		exit $$? ; \
	done

%_only:
	$(MAKE) -C $(@:_only=)

%_romfs:
	$(MAKE) -C $(@:_romfs=) romfs

%_clean:
	$(MAKE) -C $(@:_clean=) clean

romfs:
	for i in $(dir_y) ; do \
		[ ! -d $$i ] || \
		$(MAKE) -C $$i romfs ; \
	done

clean:
	for i in `ls -d *` ; do \
		[ ! -d $$i ] || \
		$(MAKE) -C $$i clean ; \
	done
