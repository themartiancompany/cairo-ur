# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.12.6
pkgrel=2
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'libxext' 'fontconfig' 'pixman' 'glib2' 'sh')
makedepends=('librsvg' 'poppler-glib' 'libspectre' 'gtk-doc') # 'libdrm')
optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
options=('!libtool')
source=(http://cairographics.org/releases/$pkgname-$pkgver.tar.xz
        cairo-1.10.0-buggy_gradients.patch
        git_fixes.diff)
sha1sums=('a383c6cb4495e18848ea43e1031c294aa9417a43'
          '8b843a9934e5112b6188e5bcf4adfc1fdaf9fa04'
          '31b3179cda0afa2e2f037d6850fd8607383cb95a')

build() {
  cd "$srcdir/$pkgname-$pkgver"
#  patch -Np1 -i ${srcdir}/cairo-1.10.0-buggy_gradients.patch

  # status: http://cgit.freedesktop.org/cairo/commit/?id=66625cb46c985321c46b79d2163a4d676d6700ba
  # 2012-10-30 12:40:41 (GMT)
  # xlib: Apply the image offsets to the destination rather the source
  patch -Np1 -i ${srcdir}/git_fixes.diff

#  autoreconf -vfi
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
#  make -k check || /bin/true # 161 Passed, 328 Failed [8 crashed, 10 expected], 26 Skipped
#}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make DESTDIR="$pkgdir" install
}
