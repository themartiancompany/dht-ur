#
#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.
#

#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Brett Cornwall <ainola@archlinux.org>
# Contributor: Solomon Choina <shlomochoina@gmail.com>

_pkg=dht
pkgname="${_pkg}"
pkgver=0.27
pkgrel=5
pkgdesc='BitTorrent DHT library'
arch=(
  'x86_64'
)
_http="https://github.com"
_ns="jech"
url="${_http}/${_ns}/${_pkg}"
license=(
  "MIT"
)
makedepends=(
  "cmake"
)
_dht_cmake_patch_uri="${_http}/transmission/${_pkg}/commit/b02da598.patch"
source=(
  "${url}/archive/refs/tags/${_pkg}-${pkgver}.tar.gz"
  "dht-cmake.patch::https://github.com/transmission/dht/commit/b02da598.patch"
)
sha256sums=('caba469a784a5c359c084099fdc025cfe09b1faec2ba9ba257b7384351c43c0a'
            '91fb75029bf04456bb7fd9c7cc14d544e906d35a309cc8de5be081049aeb7649')

prepare() {
  patch -d dht-dht-$pkgver -p1 < dht-cmake.patch # Add cmake support
}

build() {
  cmake -B build -S dht-dht-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_INCLUDEDIR=include/dht \
    -DCMAKE_C_FLAGS="$CFLAGS -ffat-lto-objects"
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
  install -Dm644 dht-dht-$pkgver/LICENCE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

