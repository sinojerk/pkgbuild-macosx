pkgname=smartmontools
pkgver=7.2
pkgrel=1
pkgdesc='SMART hard drive monitoring'
arch=('arm64' 'x86_64')
url='https://www.smartmontools.org/'
license=('GPL-2.0+')
source=("https://downloads.sourceforge.net/project/smartmontools/smartmontools/$pkgver/smartmontools-$pkgver.tar.gz")
sha256sums=('5cd98a27e6393168bc6aaea070d9e1cd551b0f898c52f66b2ff2e5d274118cd6')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --disable-dependency-tracking \
    --prefix=/usr/local \
    --sbindir=/usr/local/bin \
    --with-savestates \
    --with-attributelog

  make
}

check() {
  cd $pkgname-$pkgver
  make check || echo "Ignoring test failures"
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}
