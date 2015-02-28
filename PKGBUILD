# $Id: PKGBUILD 117894 2014-08-26 08:57:35Z bluewind $
# Maintainer: Andreas Radke <andyrtr@archlinux.org>

_pkgbasename=libgcrypt
pkgname=lib32-$_pkgbasename
pkgver=1.6.2
pkgrel=1
pkgdesc="General purpose cryptographic library based on the code from GnuPG (32-bit)"
arch=(x86_64)
url="http://www.gnupg.org"
license=('LGPL')
depends=('lib32-libgpg-error>=1.10-2' $_pkgbasename)
makedepends=(gcc-multilib libtool-multilib)
source=(ftp://ftp.gnupg.org/gcrypt/${_pkgbasename}/${_pkgbasename}-${pkgver}.tar.bz2)
sha1sums=('cc31aca87e4a3769cb86884a3f5982b2cc8eb7ec')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd ${_pkgbasename}-${pkgver}

  # Use 32-bit assembler
  sed 's:path="amd64":path="i586 i386":' -i mpi/config.links

  ./configure --prefix=/usr --disable-static --disable-padlock-support \
              --libdir=/usr/lib32 --enable-shared
  make
}

package() {
  cd ${_pkgbasename}-${pkgver}

  make DESTDIR=${pkgdir} install
  rm -rf "${pkgdir}"/usr/{include,share,bin,sbin}
}
