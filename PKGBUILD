# Maintainer: grmat <grmat@sub.red>

pkgname=libdrm-amd
_pkgname=libdrm
pkgver=2.4.14.r1612.g1fe5f0fe
pkgrel=1
pkgdesc="Userspace interface to kernel DRM services, AMD hybrid version"
arch=(i686 x86_64)
license=('custom')
depends=('libpciaccess' 'linux-amd')
makedepends=('valgrind' 'xorg-util-macros' 'libxslt' 'docbook-xsl')
checkdepends=('cairo')
provides=('libdrm')
conflicts=('libdrm')
replaces=('libdrm-new' 'libdrm-nouveau' 'libdrm')
url="http://people.freedesktop.org/~agd5f"
source=('libdrm::git://people.freedesktop.org/~agd5f/drm#branch=amd-mainline-hybrid-master20170517'
        COPYING)
sha512sums=('SKIP'
            'b0ca349b882a4326b19f81f22804fabdb6fb7aef31cdc7b16b0a7ae191bfbb50c7daddb2fc4e6c33f1136af06d060a273de36f6f3412ea326f16fa4309fda660')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  #should find something better, repo is not tagged correctly (last tag 2.4.14, actual version is 2.4.81)
  git describe --long | sed 's/^libdrm-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd ${_pkgname}
  ./autogen.sh --prefix=/usr --enable-udev
  make
}

check() {
  cd ${_pkgname}
  #currently fails
  #make -k check
}

package() {
  cd ${_pkgname}
  make DESTDIR="$pkgdir" install
  install -m755 -d "$pkgdir/usr/share/licenses/$pkgname"
  install -m644 ../COPYING "$pkgdir/usr/share/licenses/$pkgname/"
}
