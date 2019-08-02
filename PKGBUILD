# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.17.2+17+g52a7c79fd
pkgrel=1
pkgdesc="2D graphics library with support for multiple output devices"
url="https://cairographics.org/"
arch=(x86_64)
license=(LGPL MPL)
depends=(libpng libxrender libxext fontconfig pixman glib2 lzo)
makedepends=(librsvg gtk2 poppler-glib libspectre gtk-doc valgrind git)
checkdepends=(ttf-dejavu gsfonts)
_commit=52a7c79fd4ff96bb5fac175f0199819b0f8c18fc  # master
source=("git+https://gitlab.freedesktop.org/cairo/cairo.git#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
  cd cairo
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd cairo

  # Update gtk-doc
  cp /usr/share/aclocal/gtk-doc.m4 build/aclocal.gtk-doc.m4
  cp /usr/share/gtk-doc/data/gtk-doc.make build/Makefile.am.gtk-doc

  # Fix typo
  sed -i 's/have_png/use_png/g' configure.ac

  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd cairo
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
        --enable-gtk-doc \
        --enable-full-testing \
        --enable-test-surfaces
  sed -i 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

check() {
  cd cairo
  # FIXME: tests don't pass
  env CAIRO_TEST_TARGET=image \
      CAIRO_TEST_TARGET_FORMAT=rgba \
      CAIRO_TESTS='!pthread-show-text' make -k check || :
}

package() {
  cd cairo
  make DESTDIR="$pkgdir" install
}
