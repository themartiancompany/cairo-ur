# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.15.14
pkgrel=1
pkgdesc="2D graphics library with support for multiple output devices"
url="https://cairographics.org/"
arch=(x86_64)
license=(LGPL MPL)
depends=(libpng libxrender libxext fontconfig pixman glib2 lzo)
makedepends=(librsvg gtk2 poppler-glib libspectre gtk-doc valgrind git)
_commit=d9aaea0c1e1484c632e1a6735c6ecc961c4b032b  # tags/1.15.14^0
source=("git+https://gitlab.freedesktop.org/cairo/cairo.git#commit=$_commit")
sha1sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd $pkgname

  # Update gtk-doc
  cp /usr/share/aclocal/gtk-doc.m4 build/aclocal.gtk-doc.m4
  cp /usr/share/gtk-doc/data/gtk-doc.make build/Makefile.am.gtk-doc

  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd $pkgname
  ./configure --prefix=/usr \
        --sysconfdir=/etc \
        --localstatedir=/var \
        --disable-static \
        --disable-gl \
        --enable-tee \
        --enable-svg \
        --enable-ps \
        --enable-pdf \
        --enable-gobject \
        --enable-gtk-doc
        #--enable-full-testing \
        #--enable-test-surfaces
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

check() {
  cd $pkgname
  # many tests in cairo-test-suite hang forever
  # xvfb-run make check
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
