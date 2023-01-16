emerge cpuid2cpuflags <br />
echo "*/* $(cpuid2cpuflags)" > /etc/portage/package.use/00cpu-flags <br />

mkdir -p /etc/portage/env && cp -v compiler-gcc /etc/portage/env/compiler-gcc <br />

echo "sys-libs/efivar compiler-gcc" >> /etc/portage/package.env <br />
echo "dev-libs/jansson compiler-gcc" >> /etc/portage/package.env <br />

echo "sys-devel/gcc ~amd64" >> /etc/portage/package.accept_keywords/zfs <br />
echo "sys-kernel/spl ~amd64" >> /etc/portage/package.accept_keywords/zfs <br />
echo "sys-fs/zfs ~amd64" >> /etc/portage/package.accept_keywords/zfs <br />
echo "sys-fs/zfs-kmod ~amd64" >> /etc/portage/package.accept_keywords/zfs <br />
echo "sys-boot/grub ~amd64" >> /etc/portage/package.accept_keywords/zfs <br />

emerge --ask --oneshot sys-devel/gcc <br />

gcc-config --list-profiles <br />

gcc-config set 2 <br />

source /etc/profile <br />
emerge --ask --oneshot --usepkg=n sys-devel/libtool <br />
emerge --ask --depclean sys-devel/gcc <br />

emerge --ask --verbose --emptytree --usepkg=n --update --deep --newuse @world 
