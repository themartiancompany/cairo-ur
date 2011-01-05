# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.10.2
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng>=1.4.0' 'libxrender' 'fontconfig>=2.8.0' 'pixman>=0.18.4' 'glib2>=2.24.0')
makedepends=('pkgconfig')
options=('!libtool')
source=(http://cairographics.org/releases/${pkgname}-${pkgver}.tar.gz
        cairo-1.10.0-buggy_gradients.patch)
sha1sums=('ccce5ae03f99c505db97c286a0c9a90a926d3c6e'
          '8b843a9934e5112b6188e5bcf4adfc1fdaf9fa04')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -Np1 -i "${srcdir}/cairo-1.10.0-buggy_gradients.patch"
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --disable-static
  make
  make DESTDIR="${pkgdir}" install
}
