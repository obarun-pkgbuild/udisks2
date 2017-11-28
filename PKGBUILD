# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/udisks2
# 						Maintainer: Ionut Biru <ibiru@archlinux.org>

pkgname=udisks2
pkgver=2.7.4
pkgrel=2
pkgdesc="Disk Management Service, version 2"
arch=('x86_64')
url="https://www.freedesktop.org/wiki/Software/udisks"
license=('GPL2')
depends=('polkit' 'libatasmart' 'libgudev' 'libblockdev' 'dbus')
makedepends=('docbook-xsl' 'gobject-introspection' 'gnome-common' 'intltool' 'parted' 'which' 'gettext' 'gtk-doc' 'libxslt') # 'open-iscsi' 
optdepends=('gptfdisk: GUID partition table support'
            'ntfs-3g: NTFS filesystem management support'
            'dosfstools: VFAT filesystem management support'
            'libiscsi: iSCSI support')
#commit=c7ef3361a1bc45e43a155640f7b80b55349a1339 # tag 2.7.3
source=("https://github.com/storaged-project/udisks/archive/udisks-$pkgver.tar.gz")
md5sums=('a579c4b7e151fc33e0a97fb1db80eed5')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

build() {
  cd udisks-udisks-$pkgver
  ./autogen.sh 	--prefix=/usr \
				--sysconfdir=/etc \
				--sbindir=/usr/bin \
				--libexecdir=/usr/lib \
				--localstatedir=/var \
				--disable-static \
				--enable-gtk-doc-html=yes
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
#gtk-doc 1.25
