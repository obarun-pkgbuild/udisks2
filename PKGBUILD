# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/udisks2
# 						Maintainer: Ionut Biru <ibiru@archlinux.org>

pkgname=udisks2
pkgver=2.7.1
pkgrel=3
pkgdesc="Disk Management Service, version 2"
arch=('x86_64')
url="https://www.freedesktop.org/wiki/Software/udisks"
license=('GPL2')
depends=('polkit' 'libatasmart' 'libgudev' 'libblockdev')
makedepends=('docbook-xsl' 'gobject-introspection' 'gnome-common' 'intltool' 'parted' 'libiscsi' 'which' 'gettext')
optdepends=('gptfdisk: GUID partition table support'
            'ntfs-3g: NTFS filesystem management support'
            'dosfstools: VFAT filesystem management support'
            'libiscsi: iSCSI support')
source=("https://github.com/storaged-project/udisks/archive/udisks-$pkgver.tar.gz")
sha512sums=('1f6830bcea0d26aeb63a54437f92756e2fecc35953d985469b01067774bed8d7bbff1edb2f09a451ae1929d299c6015a4c0aea3b0dc01cc36bd4759685dcf55b')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  sed -e 's/AC_MSG_ERROR(\[libstoragemgmt/AC_MSG_WARN([libstoragemgmt/' \
      -e 's/AC_MSG_ERROR(\[libconfig/AC_MSG_WARN([libconfig/' \
      -i udisks-udisks-$pkgver/configure.ac
}

build() {
  cd udisks-udisks-$pkgver
  ./autogen.sh 	--prefix=/usr \
				--sysconfdir=/etc \
				--sbindir=/usr/bin \
				--libexecdir=/usr/lib \
				--localstatedir=/var \
				--disable-static \
				--disable-systemd \
				--enable-compile-warnings=minimum \
				--localstatedir=/var \
				--enable-available-modules
	make
}

check() {
  cd udisks-udisks-$pkgver
  make check
}

package() {
  cd udisks-udisks-$pkgver
  make DESTDIR="$pkgdir" install \
    bash_completiondir=/usr/share/bash-completion/completions
}
