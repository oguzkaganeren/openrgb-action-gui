# Maintainer: Oguz Kaganer Eren <oguzkaganeren@gmail.com>

pkgname=openrgb-ruler-git
pkgver=r17.f714d1a
pkgrel=1
pkgdesc="GUI for automated RGB lighting control rules via OpenRGB"
arch=('x86_64' 'aarch64')
url="https://github.com/oguzkaganeren/openrgb-ruler"
license=('GNU')
depends=(
  'cairo'
  'desktop-file-utils'
  'gdk-pixbuf2'
  'glib2'
  'gtk3'
  'hicolor-icon-theme'
  'libsoup'
  'pango'
  'webkit2gtk-4.1'
  'openrgb'
)
makedepends=(
  'git'
  'rust'
  'cargo'
  'nodejs'
  'yarn'
  'openssl'
  'libappindicator-gtk3'
  'librsvg'
  'appmenu-gtk-module'
)
provides=('openrgb-ruler')
conflicts=('openrgb-ruler')
install=${pkgname%-git}.install
source=("git+${url}.git")
sha256sums=('SKIP')

pkgver() {
  cd openrgb-ruler
  (
    set -o pipefail
    git describe --long --abbrev=7 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
      printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
  )
}

prepare() {
  cd openrgb-ruler
  yarn install --frozen-lockfile
}

build() {
  cd openrgb-ruler
  yarn tauri build -b deb
}

package() {
  cd openrgb-ruler
  cp -a src-tauri/target/release/bundle/deb/openrgb-ruler_*/data/. "${pkgdir}"
}
