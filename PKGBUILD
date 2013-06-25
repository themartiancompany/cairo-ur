# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.12.14
pkgrel=4
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'libxext' 'fontconfig' 'pixman>=0.28.0' 'glib2' 'mesa>=9.1' 'libgl' 'sh' 'lzo2')
makedepends=('mesa-libgl>=9.1' 'librsvg' 'gtk2' 'poppler-glib' 'libspectre' 'gtk-doc' 'valgrind'
             # for the test suite:
             'ttf-dejavu' 'gsfonts' 'xorg-server-xvfb' ) # 'libdrm')
#optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
options=('!libtool')
source=(http://cairographics.org/releases/$pkgname-$pkgver.tar.xz
        libpng16.patch)
sha1sums=('9106ab09b2e7b9f90521b18dd4a7e9577eba6c15'
          'c9911f185637d266ce1d2985bd6fb7d0df3d75b2')

build() {
  cd $pkgname-$pkgver

  patch -Np1 -i ../libpng16.patch

  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--localstatedir=/var \
	--disable-static \
	--enable-tee \
	--enable-gl \
	--enable-egl \
	--enable-svg \
	--enable-ps \
	--enable-pdf \
	--enable-gobject #\
	# --enable-test-surfaces
	
	#--disable-xlib-xcb \
	# --enable-test-surfaces \ takes ages
	#--enable-drm # breaks build
	
  make
}

#check() {
#  cd "$srcdir/$pkgname-$pkgver"
  #make -k check || /bin/true # 162 Passed, 328 Failed [8 crashed, 10 expected], 26 Skipped
#  make test || /bin/true # 29 Passed, 464 Failed [460 crashed, 2 expected], 26 Skipped
#}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}
