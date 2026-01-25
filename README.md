### Actions-OpenWrt
#
- Debian 11 或 Ubuntu LTS
- 安装编译依赖

   ```bash
   sudo apt update -y
   sudo apt full-upgrade -y
   sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache clang cmake cpio curl device-tree-compiler flex gawk gcc-multilib g++-multilib gettext \
genisoimage git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libfuse-dev libglib2.0-dev \
libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libpython3-dev \
libreadline-dev libssl-dev libtool llvm lrzsz libnsl-dev ninja-build p7zip p7zip-full patch pkgconf \
python3 python3-pyelftools python3-setuptools qemu-utils rsync scons squashfs-tools subversion \
swig texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
   ```

- 下载源代码，更新 feeds

   ```bash
   git clone https://github.com/coolsnowwolf/lede openwrt
   cd openwrt
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   ```

- 更改默认IP、空密码、固件信息
  ```bash
  sed -i 's/192.168.1.1/192.168.100.10/g' package/base-files/luci2/bin/config_generate
  sed -i '/CYXluq4wUazHjmCDBCqXF/d' package/lean/default-settings/files/zzz-default-settings
  sed -i "s/LEDE /Z-turn /g" package/lean/default-settings/files/zzz-default-settings
  ```

- 选择配置
  ```bash
  make menuconfig
  ```
  ```
  Extra packages中  勾选ipv6helper
  Network----Firewall---ip6tables 勾选全部
  ```
  
- 下载dl库，编译固件
  ```bash
  make -j8 download V=s
  make V=s -j$(nproc)
  ```
  
#
### 感谢 ❤️  [Lean源码](https://github.com/coolsnowwolf/lede) | [P3TERX云编译](https://github.com/P3TERX/Actions-OpenWrt)  
