# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.8.8
pkgrel=2
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng>=1.4.0' 'libxrender' 'fontconfig>=2.8.0' 'pixman>=0.16.4' 'xcb-util>=0.3.6')
makedepends=('pkgconfig' 'gtk-doc')
options=('!libtool')
source=(http://cairographics.org/releases/${pkgname}-${pkgver}.tar.gz)
md5sums=('d3e1a1035ae563812d4dd44a74fb0dd0')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  sed -i -e 's/libpng13/libpng14/g' configure || return 1
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --enable-xcb --disable-static || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1
}
