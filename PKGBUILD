# Maintainer: Edward Davis <idlyby@proton.me>
# Contributor: alba4k <blaskoazzolaaaron@gmail.com>

_pkgname="hypridle"
pkgname="${_pkgname}-git"
pkgver=0.1.1.r4.gdad6ac14
pkgrel=1
pkgdesc="Hyprland's idle daemon"
arch=(any)
url="https://github.com/hyprwm/hypridle"
license=('BSD-3-Clause')
depends=('wayland' 'hyprlang-git' 'sdbus-cpp-git' 'systemd' 'wayland-protocols' 'hyprutils-git')
makedepends=('git' 'cmake' 'gcc' 'gdb' 'xorgproto')
source=("${_pkgname}::git+https://github.com/hyprwm/hypridle.git")
provides=("hypridle")
conflicts=("hypridle")
sha256sums=('SKIP')

pkgver() {
	cd ${_pkgname}
    git describe --long --tags --abbrev=8 --exclude='*[a-zA-Z][a-zA-Z]*' \
      | sed -E 's/^[^0-9]*//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
	cd "${srcdir}/${_pkgname}"
	cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX=/usr -S . -B ./build
    cmake --build ./build --config Release --target hypridle
}

package() {
	cd "${srcdir}/${_pkgname}"
	DESTDIR="${pkgdir}" cmake --install build

	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
