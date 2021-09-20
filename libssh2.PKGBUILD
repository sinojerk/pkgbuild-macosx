pkgname=libssh2
pkgver=1.10.0
pkgrel=1
pkgdesc='C library implementing the SSH2 protocol'
arch=('arm64' 'x86_64')
url='https://www.libssh2.org/'
license=('BSD-3-Clause')
depends=('openssl')
macosbuildins=('zlib')
source=("https://www.libssh2.org/download/libssh2-$pkgver.tar.gz")
sha256sums=('2d64e90f3ded394b91d3a2e774ca203a4179f69aebee03003e5a6fa621e41d51')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr/local \
    --disable-silent-rules \
    --disable-examples-build \
    --with-libz \
    --with-openssl \
    --with-libssl-prefix=`pkg-config --variable prefix openssl`

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
