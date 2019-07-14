_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede-lts
pkgver=0.1.0
pkgdesc="Kernel module for deepin-anything (linux-bede-lts)"
_extramodules=4.19-BEDE-LTS-external
_current_linux_version=4.19.59
_next_linux_version=4.20
pkgrel=15
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
sha512sums=('892828f7c52bb267993507890329e3f3b03550dd5a575a61a70995ce5d9f8cd27f1f1e5b21d4a1ec213ffc430d5236102a9e49b98a0fc0bf2f9042e719d9bfde')

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

