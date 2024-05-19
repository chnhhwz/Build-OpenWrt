# Actions-OpenWrt

- root  @  192.168.100.100
- ArgonTheme | OpenClash | SSRP+ | AccessControl | AliDNS | MsdLite | WOL | FrpS/C | UPnP | Vlmcsd | Qos | Eqos
- ❤️  [Lean](https://github.com/coolsnowwolf/lede) |  [P3TERX](https://github.com/P3TERX/Actions-OpenWrt)  |  [honwen](https://github.com/honwen/luci-app-aliddns) |  [ximiTech ](https://github.com/ximiTech)  |  [jerrykuku](https://github.com/jerrykuku)
#
### 在本地机器上配置.config:
1. 安装编译依赖

   ```bash
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
   bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
   git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libfuse-dev libglib2.0-dev libgmp3-dev \
   libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libpython3-dev libreadline-dev \
   libssl-dev libtool lrzsz mkisofs msmtp ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 \
   python3-pyelftools python3-setuptools qemu-utils rsync scons squashfs-tools subversion swig texinfo \
   uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
   ```

2. 下载源代码，更新 feeds 并选择配置

   ```bash
   git clone https://github.com/coolsnowwolf/lede openwrt
   cd openwrt
   #
   # SSR Plus+
   sed -i 's/^#\(.*helloworld\)/\1/' feeds.conf.default
   #
   # OpenClash
   echo 'src-git openclash https://github.com/vernesong/OpenClash' >>feeds.conf.default
   #
   # luci-app-msd_lite
   cd package/lean
   git clone https://github.com/ximiTech/luci-app-msd_lite.git
   #
   # luci-app-aliddns
   cd ~/openwrt
   mkdir -p package/feeds
   git clone https://github.com/honwen/luci-app-aliddns.git package/feeds/luci-app-aliddns
   #
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   #
   # msd_lite
   rm -rf feeds/packages/net/msd_lite
   git clone https://github.com/ximiTech/msd_lite.git feeds/packages/net/msd_lite
   #
   # ArgonTheme
   rm -rf feeds/luci/themes/luci-theme-argon
   git clone -b 18.06 https://github.com/jerrykuku/luci-theme-argon.git feeds/luci/themes/luci-theme-argon
   rm -rf feeds/luci/applications/luci-app-argon-config
   git clone https://github.com/jerrykuku/luci-app-argon-config.git feeds/luci/applications/luci-app-argon-config
   #
   make menuconfig
   ```

3. 复制并上传.config
