# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
#_gitdate=20120426
#_gitver=957a9cc619965178a8927d114fe852034fc2385c
pkgver=1.12.2
pkgrel=1
pkgdesc="Cairo vector graphics library"
arch=(i686 x86_64)
license=('LGPL' 'MPL')
url="http://cairographics.org/"
depends=('libpng' 'libxrender' 'fontconfig' 'pixman' 'glib2' 'sh')
makedepends=('librsvg' 'poppler-glib' 'libspectre' 'gtk-doc') # 'libdrm')
optdepends=('xcb-util: for XCB backend') # really needed?
provides=('cairo-xcb')
replaces=('cairo-xcb')
options=('!libtool')
source=(http://cairographics.org/releases/$pkgname-$pkgver.tar.xz
        #$pkgname-$pkgver.tar.gz::http://cgit.freedesktop.org/cairo/snapshot/cairo-${_gitver}.tar.gz 
        cairo-1.10.0-buggy_gradients.patch
        #git_fixes.patch 
)
md5sums=('87649eb75789739d517c743e94879e51'
         '9b323790dab003e228c6955633cb888e')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  #cd ${srcdir}/${pkgname}-${_gitver}
  patch -Np1 -i ${srcdir}/cairo-1.10.0-buggy_gradients.patch
  # status is 2012-04-26 last commit: image: Fix typo in _blit_spans()
  #patch -Np1 -i ${srcdir}/git_fixes.patch
  autoreconf -vfi
  #./autogen.sh --prefix=/usr \
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
#  #cd "$srcdir/$pkgname-$pkgver"
#  cd $srcdir/$pkgname-${_gitver}
#  make -k check || /bin/true # 165 Passed, 316 Failed [3 crashed, 10 expected], 23 Skipped
#}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  #cd $srcdir/$pkgname-${_gitver}
  make DESTDIR="$pkgdir" install
}
