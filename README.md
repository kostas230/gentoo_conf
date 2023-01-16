# Microcode optimizations

emerge cpuid2cpuflags
echo "*/* $(cpuid2cpuflags)" > /etc/portage/package.use/00cpu-flags

# Set GCC as fallback compiler 

mkdir -p /etc/portage/env && cp -v compiler-gcc /etc/portage/env/compiler-gcc

echo "sys-libs/efivar" >> /etc/portage/package.env
echo "dev-libs/jansson" >> /etc/portage/package.env
echo "sys-devel/gcc" >> /etc/portage/package.env

#Latest version for GCC, GRUB, ZFS

echo "sys-devel/gcc ~amd64" >> /etc/portage/package.accept_keywords/zfs
echo "sys-kernel/spl ~amd64" >> /etc/portage/package.accept_keywords/zfs
echo "sys-fs/zfs ~amd64" >> /etc/portage/package.accept_keywords/zfs
echo "sys-fs/zfs-kmod ~amd64" >> /etc/portage/package.accept_keywords/zfs
echo "sys-boot/grub ~amd64" >> /etc/portage/package.accept_keywords/zfs

# Upgrade GCC
emerge --ask --oneshot sys-devel/gcc

gcc-config --list-profiles

# $N is the new gcc version
gcc-config set $N
source /etc/profile
emerge --ask --oneshot --usepkg=n sys-devel/libtool
emerge --ask --depclean sys-devel/gcc

# Upgrade everything
emerge --ask --verbose --emptytree --usepkg=n --update --deep --newuse @world @world

