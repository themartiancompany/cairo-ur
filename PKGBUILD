# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.13.1
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'libxext' 'fontconfig' 'pixman>=0.28.0' 'glib2' 'mesa' 'libgl' 'lzo')
makedepends=('mesa-libgl' 'librsvg' 'gtk2' 'poppler-glib' 'libspectre' 'gtk-doc' 'valgrind' 'git')
             # for the test suite:
             #'ttf-dejavu' 'gsfonts' 'xorg-server-xvfb' ) # 'libdrm')
#optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
source=('git://anongit.freedesktop.org/cairo#commit=29a8b4e970379ca04a7db8e63c71bb34c0e349ce')
sha1sums=('SKIP')

build() {
  cd $pkgname
  NOCONFIGURE=1 ./autogen.sh

  ./configure --prefix=/usr \
	--sysconfdir=/etc \
	--localstatedir=/var \
	--disable-static \
	--disable-lto \
	--enable-tee \
	--enable-gl \
	--enable-egl \
	--enable-svg \
	--enable-ps \
	--enable-pdf \
	--enable-gobject \
        --enable-gtk-doc #\
	# --enable-test-surfaces
	
	#--disable-xlib-xcb \
	# --enable-test-surfaces \ takes ages
	#--enable-drm # breaks build
	
  make
}

check() {
  cd $pkgname
  #make -j1 -k test || /bin/true
  
  # results:
  # 1.12.8-1	# 162 Passed, 328 Failed [8 crashed, 10 expected], 26 Skipped
  # 1.12.12-2:	# 29 Passed, 464 Failed [460 crashed, 2 expected], 26 Skipped
  # 1.12.16-1:	144 Passed, 364 Failed [6 crashed, 12 expected], 27 Skipped

}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
