# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>
# Contributor: Brice Carpentier <brice@daknet.org>
# Contributor: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Contributor: Truocolo <truocolo@aol.com>

pkgbase=cairo
pkgname=(
  "${pkgbase}"
  "${pkgbase}-docs"
)
pkgver=1.18.0
pkgrel=1
pkgdesc="2D graphics library with support for multiple output devices"
url="https://${pkgbase}graphics.org/"
arch=(
  x86_64
  arm
  armv7h
  armv6l
  aarch64
  pentium4
  i686
  powerpc)
license=(
  LGPL
  MPL
)
depends=(
  fontconfig
  freetype
  glib2
  libpng
  libx11
  libxcb
  libxext
  libxrender
  lzo
  pixman
  zlib
)
makedepends=(
  git
  gtk-doc
  meson
  valgrind
)
_commit=3909090108bb2db55330e3eb148aebe664735363  # tags/1.18.0^0
_project='freedesktop'
_http="https://gitlab.${_project}.org"
_url="${_http}/${pkgbase}/${pkgbase}"
_local="file://${HOME}/${pkgbase}"
source=(
  "git+${_url}.git#commit=$_commit" 
  # "git+${_local}#commit=$_commit"
)
b2sums=(
  'SKIP')

pkgver() {
  cd \
    "${pkgbase}"
  git \
    describe \
    --tags | \
    sed 's/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd \
    "${pkgbase}"
}

_meson_options=(
  -D dwrite=disabled
  # Upstream bug in mkhtml
  -D gtk_doc=false
  -D spectre=disabled
  -D symbol-lookup=disabled
  -D tests=disabled
  -D xlib=enabled
)

build() {
  arch-meson \
    "${pkgbase}" \
    build \
    "${_meson_options[@]}"
  meson \
    compile \
    -C build
}

package_cairo() {
  provides=(
    "lib${pkgbase}-gobject.so"
    "lib${pkgbase}-script-interpreter.so"
    "lib${pkgbase}.so"
    "lib${pkgbase}=${pkgver}"
  )

  meson \
    install \
    -C build \
    --destdir \
      "${pkgdir}"
}

package_cairo-docs() {
  pkgdesc+=" (documentation)"
  depends=()
  if [[ " ${_meson_options[*]} " =~ \
        ' gtk_doc=true ' ]] then
    mv \
      doc/* \
      "${pkgdir}"
  fi
}

# vim:set sw=2 sts=-1 et:
