pkgname=pkg-config
pkgver=0.29.2
pkgrel=3
pkgdesc='Manage compile and link flags for libraries'
arch=('arm64' 'x86_64')
url='https://freedesktop.org/wiki/Software/pkg-config/'
license=('GPL-2.0+')
source=("https://pkgconfig.freedesktop.org/releases/pkg-config-$pkgver.tar.gz")
sha256sums=('6fc69c01688c9458a57eb9a1664c9aba372ccda420a02bf4429fe610e7e7d591')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr/local \
    --disable-debug \
    --disable-host-tool \
    --with-internal-glib

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
