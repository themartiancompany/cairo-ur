# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.8.4
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng>=1.2.33' 'libxrender' 'fontconfig>=2.6.0' 'pixman>=0.12.0' 'xcb-util>=0.3.1')
makedepends=('pkgconfig')
options=('!libtool')
source=(http://cairographics.org/releases/${pkgname}-${pkgver}.tar.gz)
md5sums=('a5067e355e78294db2485aa97afd1115')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --enable-xcb --disable-static || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1
}
