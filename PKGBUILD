#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

_langname="python"
_langmajor="2"
_relname="pygobject"
_relmajor="2"
_aurname="gobject"
_commit="c9594b6a91e6ca2086fedec2ed8249e0a9c029fc" # tags/PYGOBJECT_2_28_7^0

pkgname="${_langname}${_langmajor}-${_aurname}${_relmajor}"
pkgver=2.28.6
pkgrel=1
pkgdesc="Legacy Python 2 bindings for GObject"
url="https://wiki.gnome.org/Projects/PyGObject"
arch=(
  "x86_64"
)
license=(
  "LGPL"
)
depends=(
  "glib2"
  "libffi"
  "python2"
  "gobject-introspection"
  "python2-cairo"
)
makedepends=(
  "git")
provides=(
  "pygobject2-devel=$pkgver-$pkgrel"
)
conflicts=(
  "pygobject2-devel"
)
replaces=(
  "pygobject2-devel<=2.28.7-3"
)
source=(
  "https://gitlab.gnome.org/GNOME/${_relname}/-/archive/PYGOBJECT_2_28_6/${_relname}-PYGOBJECT_2_28_6.tar.gz"
)
sha512sums=(
  "29efccbfe998f8ad461111b6a4ed65f39f621c700ad4047602dc94de3dfd95927d71cab9b13f6bdfaa984fd0e0864c0c4f604516bb283cf00421190b2d3d2d22"
)


prepare() {

  cd "${_relname}-PYGOBJECT_2_28_6"

find . \( -name '*.py' -o -name '*.py.in' \) -exec sed -i '1s|python$|&2|' {} +
  
  autoreconf -fvi

}

build() (

  cd "${_relname}-PYGOBJECT_2_28_6"

  CPPFLAGS+=' -Wno-deprecated-declarations'

  ./configure --prefix=/usr --disable-introspection PYTHON=/usr/bin/python2

   sed -i 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make
)

package() {

  cd "${_relname}-PYGOBJECT_2_28_6"

  make DESTDIR="$pkgdir" install

}
