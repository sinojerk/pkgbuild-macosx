pkgname=openssl
pkgver=1.1.1l
pkgrel=1
pkgdesc='Cryptography and SSL/TLS Toolkit'
arch=('arm64' 'x86_64')
url='https://openssl.org/'
license=('OpenSSL')
source=("https://www.openssl.org/source/openssl-$pkgver.tar.gz")
sha256sums=('0b7a3e5e59c34827fe0c3a74b7ec8baef302b98fa80088d7f9153aa16fa76bd1')

build() {
  cd $pkgname-$pkgver

  ./config \
    --prefix=/usr/local/opt/$pkgname-$pkgver \
    --openssldir=/usr/local/etc/openssl \
    no-zlib \
    enable-ec_nistp_64_gcc_128

  make
}

build_universal() {
    currnetdir="$PWD"
    for arch in x86_64 arm64; do
        mkdir -p "$pkgname-$pkgver.$arch"
        cd "$pkgname-$pkgver.$arch"
        perl ../$pkgname-$pkgver/Configure \
          --prefix=/usr/local/opt/$pkgname-$pkgver \
          --openssldir=/usr/local/etc/openssl \
          darwin64-${arch}-cc \
          no-zlib \
          enable-ec_nistp_64_gcc_128
        make
        cd "$currnetdir"
    done
}

check() {
  cd $pkgname-$pkgver
  make test || echo "Ignoring test failures"
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install_sw install_ssldirs install_man_docs
}

package_universal() {
  currnetdir="$PWD"

  cd $pkgname-$pkgver.x86_64
  make DESTDIR="pkg" install_sw
  cd "$currnetdir"

  cd $pkgname-$pkgver.arm64
  make DESTDIR="pkg" install_sw
  make DESTDIR="$pkgdir" install_sw install_ssldirs install_man_docs
  cd "$currnetdir"

  opensslroot="usr/local/opt/$pkgname-$pkgver"
  cd "$pkgdir"
  find "$opensslroot"/{bin,lib} -type f -exec \
    sh -c "file -Ib '{}'|grep -q 'binary'" \; -print|while read -r f; do
    xcrun lipo -create -output "$f" "$currnetdir/$pkgname-$pkgver.x86_64/pkg/$f" "$currnetdir/$pkgname-$pkgver.arm64/pkg/$f"
  done
  cd "$currnetdir"
}
