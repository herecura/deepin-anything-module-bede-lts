_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede-lts
pkgver=5.0.1
pkgdesc="Kernel module for deepin-anything (linux-bede-lts)"
_extramodules=5.4-BEDE-LTS-external
_current_linux_version=5.4.21
_next_linux_version=5.5
pkgrel=63
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
sha512sums=('f79b4db917cce2611bd6964d00ae0e162fc500fa7ca76a987145456a9ee81296c776d2b83cf6492a4224c4e4fd95df3ad95a25c1c14d2d4e6865f5bbd639be14')

#prepare() {
    #cd $_pkgname-$pkgver
#}

build() {
    cd $_pkgname-$pkgver
    make -C kernelmod kdir=/usr/src/linux-bede-lts
}

package() {
    cd $_pkgname-$pkgver/kernelmod
    local extradir="/usr/lib/modules/$(</usr/src/linux-bede-lts/version)/extramodules"
    install -Dm644 vfs_monitor.ko "${pkgdir}${extradir}/$pkgname/vfs_monitor.ko"
    find "${pkgdir}" -name '*.ko' -exec xz {} +
}

