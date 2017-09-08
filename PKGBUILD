# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.15.8
pkgrel=1
pkgdesc="2D graphics library with support for multiple output devices"
url="https://cairographics.org/"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
depends=('libpng' 'libxrender' 'libxext' 'fontconfig' 'pixman' 'glib2' 'lzo')
makedepends=('librsvg' 'gtk2' 'poppler-glib' 'libspectre' 'gtk-doc' 'valgrind' 'git')
source=(https://cairographics.org/snapshots/cairo-$pkgver.tar.xz)
sha1sums=('07cc2031b74d758299eeee3ec49ecbfbfb85f1c6')

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr \
        --sysconfdir=/etc \
        --localstatedir=/var \
        --disable-static \
        --disable-lto \
        --disable-gl \
        --enable-tee \
        --enable-svg \
        --enable-ps \
        --enable-pdf \
        --enable-gobject \
        --enable-gtk-doc
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}
