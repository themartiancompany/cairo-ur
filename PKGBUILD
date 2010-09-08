# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.10.0
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng>=1.4.0' 'libxrender' 'fontconfig>=2.8.0' 'pixman>=0.18.4' 'glib2>=2.24.0')
makedepends=('pkgconfig')
options=('!libtool')
source=(http://cairographics.org/releases/${pkgname}-${pkgver}.tar.gz)
sha1sums=('efe7e47408d5188690228ccadc8523652f6bf702')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --disable-static
  make
  make DESTDIR="${pkgdir}" install
}
