# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.12.10
pkgrel=2
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'libxext' 'fontconfig' 'pixman>=0.28.0' 'glib2' 'sh')
makedepends=('librsvg' 'poppler-glib' 'libspectre' 'gtk-doc' 'valgrind') # 'libdrm')
optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
options=('!libtool')
source=(http://cairographics.org/releases/$pkgname-$pkgver.tar.xz
  	revert-xlib-map-to-image-requires-an-extents.patch
  	revert-xlib-Simplify-source-creation-by-use-of-map-to-image.patch)
sha1sums=('be06d5aaa272bbbd08380f71ca710d5612881493'
          '8bc096dd16a885ad041cb2137a64757f32d1cc88'
          'fd8ffd9aba3679c344e4f25494f199a51b0ae62c')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -Np1 -R -i ../revert-xlib-map-to-image-requires-an-extents.patch
  patch -Np1 -R -i ../revert-xlib-Simplify-source-creation-by-use-of-map-to-image.patch
  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--localstatedir=/var \
	--disable-static \
	--enable-tee \
	--disable-xlib-xcb \
	# --enable-test-surfaces \ takes ages
	#--enable-drm # breaks build
  make
}

#check() {
#  cd "$srcdir/$pkgname-$pkgver"
#  make -k check || /bin/true # 162 Passed, 328 Failed [8 crashed, 10 expected], 26 Skipped
#}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install
}
