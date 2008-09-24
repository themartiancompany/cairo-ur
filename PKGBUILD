# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.7.6
pkgrel=2
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng>=1.2.31' 'libxrender' 'fontconfig>=2.6.0' 'pixman>=0.12.0' 'xcb-util>=0.3.0')
makedepends=('pkgconfig')
options=('!libtool')
source=(http://cairographics.org/snapshots/${pkgname}-${pkgver}.tar.gz)
md5sums=('c612f581b18903b0751a171685fc38dd')

build() {
  cd ${startdir}/src/${pkgname}-${pkgver}
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --enable-xcb --disable-static || return 1
  make || return 1
  make DESTDIR=${startdir}/pkg install || return 1
}
