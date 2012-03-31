# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.12.0
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'fontconfig' 'pixman' 'glib2' 'sh')
makedepends=('librsvg' 'poppler-glib' 'libspectre') # 'libdrm')
optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
options=('!libtool')
source=(http://cairographics.org/releases/$pkgname-$pkgver.tar.gz
        cairo-1.10.0-buggy_gradients.patch)
md5sums=('e6c85575ba7094f88b637bdfd835a751'
         '9b323790dab003e228c6955633cb888e')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -Np1 -i "${srcdir}/cairo-1.10.0-buggy_gradients.patch"
  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--localstatedir=/var \
	--disable-static \
	--enable-tee \
	--enable-xlib-xcb \
	# --enable-test-surfaces \ takes ages
	#--enable-drm # breaks build
  make
}

#check() {
#  cd "$srcdir/$pkgname-$pkgver"
#  make check || /bin/true # 248 Passed, 65 Failed [2 crashed, 8 expected], 28 Skipped
#}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install
}
