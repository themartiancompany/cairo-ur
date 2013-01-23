# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.12.10
pkgrel=3
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
        xlib_Do_not_upload_the_whole_image_just_because_we_want_an_entire_row.patch)
sha1sums=('be06d5aaa272bbbd08380f71ca710d5612881493'
          '0631cc80b7512275d2be1d7d41497384013963ed')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -Np1 -i ${srcdir}/xlib_Do_not_upload_the_whole_image_just_because_we_want_an_entire_row.patch
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
