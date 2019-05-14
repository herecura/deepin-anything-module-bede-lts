_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede-lts
pkgver=0.0.8
pkgdesc="Kernel module for deepin-anything (linux-bede-lts)"
_extramodules=4.19-BEDE-LTS-external
_current_linux_version=4.19.43
_next_linux_version=4.20
pkgrel=8
arch=('x86_64')
url="https://github.com/linuxdeepin/deepin-anything"
license=('GPL3')
makedepends=(
    "linux-bede-lts>=$_current_linux_version"
    "linux-bede-lts-headers>=$_current_linux_version"
    "linux-bede-lts<$_next_linux_version"
    "linux-bede-lts-headers<$_next_linux_version"
)
depends=(
    "linux-bede-lts>=$_current_linux_version"
    "linux-bede-lts<$_next_linux_version"
)
provides=('DEEPIN-ANYTHING-MODULE')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/linuxdeepin/deepin-anything/archive/$pkgver.tar.gz")
sha512sums=('362cb94124daae214bf477179ff19177501938b8fb7972bbc208486cd24c7712e13f0ebe2d47df4583fe2d0735734282ee8461c57323b2dd3b8d2827b2b180b6')

#prepare() {
    #cd $_pkgname-$pkgver
#}

build() {
    _kernver="$(cat /usr/lib/modules/${_extramodules}/version)"

    cd $_pkgname-$pkgver
    make -C kernelmod kdir=/usr/lib/modules/$_kernver/build
}

package() {
    cd $_pkgname-$pkgver/kernelmod
    install -dm 755 "$pkgdir"/usr/lib/modules/$_extramodules/deepin
    install -m 644 vfs_monitor.ko "$pkgdir"/usr/lib/modules/$_extramodules/deepin/
    find "${pkgdir}" -name '*.ko' -exec xz {} +
}

