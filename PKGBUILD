# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>

pkgname=cairo
pkgver=1.17.4
pkgrel=1
pkgdesc="2D graphics library with support for multiple output devices"
url="https://cairographics.org/"
arch=(x86_64)
license=(LGPL MPL)
depends=(lzo zlib libpng fontconfig freetype2 libx11 libxext libxrender libxcb
         glib2 pixman)
makedepends=(valgrind git meson)
_commit=156cd3eaaebfd8635517c2baf61fcf3627ff7ec2  # tags/1.17.4^0
source=("git+https://gitlab.freedesktop.org/cairo/cairo.git#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
  cd cairo
  git describe --tags | sed 's/-/+/g'
}

prepare() {
  cd cairo
}

build() {
  arch-meson cairo build \
    -D spectre=disabled \
    -D tee=enabled \
    -D tests=disabled
  meson compile -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build
}
