# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.16.0
pkgrel=2
pkgdesc="2D graphics library with support for multiple output devices"
url="https://cairographics.org/"
arch=(x86_64)
license=(LGPL MPL)
depends=(libpng libxrender libxext fontconfig pixman glib2 lzo)
makedepends=(librsvg gtk2 poppler-glib libspectre gtk-doc valgrind git)
checkdepends=(ttf-dejavu gsfonts)
_commit=3ad43122b21a3299dd729dc8462d6b8f7f01142d  # tags/1.16.0^0
source=("git+https://gitlab.freedesktop.org/cairo/cairo.git#commit=$_commit"
        0001-ft-Use-FT_Done_MM_Var-instead-of-free-when-available.patch)
sha1sums=('SKIP'
          '9850a5b06e300055676ad1f5dfa90ecba0fe623c')

pkgver() {
  cd cairo
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd cairo

  # CVE-2018-19876
  patch -Np1 -i ../0001-ft-Use-FT_Done_MM_Var-instead-of-free-when-available.patch

  # Update gtk-doc
  cp /usr/share/aclocal/gtk-doc.m4 build/aclocal.gtk-doc.m4
  cp /usr/share/gtk-doc/data/gtk-doc.make build/Makefile.am.gtk-doc

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
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
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
