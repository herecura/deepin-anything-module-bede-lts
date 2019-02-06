_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede-lts
pkgver=0.0.3
pkgdesc="Kernel module for deepin-anything (linux-bede-lts)"
_extramodules=4.19-BEDE-LTS-external
_current_linux_version=4.19.20
_next_linux_version=4.20
pkgrel=9
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
source=("$_pkgname-$pkgver.tar.gz::https://github.com/linuxdeepin/deepin-anything/archive/$pkgver.tar.gz"
        linux-4.20.patch)
sha512sums=('8a506ba57d6a2ac9c9089719d18013fbde6443cb4f63de79498269e728b7e8725b4e06e7029ae2d2242aaac955c63e56c680fdd18e3fb0d72e9953a9fc5e8402'
            'dc3c85e9535cc589fdf56d265c4330519c92b5bcc406153e3162ba6ef5e799b702c394e1961132770f4f3ddd288dbbfe74a9d8056329e4585eb5a2094ffe0155')

prepare() {
    cd $_pkgname-$pkgver
    patch -p1 -i "$srcdir/linux-4.20.patch"
}

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

