# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: Alexander Fehr <pizzapunk gmail com>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>

pkgname=aria2
pkgver=1.36.0
pkgrel=1
pkgdesc='Download utility that supports HTTP(S), FTP, BitTorrent, and Metalink'
arch=('arm64' 'x86_64')
url='http://aria2.sourceforge.net/'
license=('GPL')
depends=('libssh2')
macosbuildins=('libxml2' 'zlib')
source=("https://github.com/aria2/aria2/releases/download/release-$pkgver/aria2-$pkgver.tar.xz")
sha512sums=('8203dbb75274455a78c50dd4f894e631de6931ac889f26896dceed78ec38c98cdbcf07e164744f308f2bfffeae1016beec1bfdbe8cad7f3280d11376aa0c2542')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr/local \
    --disable-dependency-tracking \
    --with-libssh2 \
    --without-gnutls \
    --without-libgmp \
    --without-libnettle \
    --without-libgcrypt \
    --with-appletls \
    --without-openssl

  make
}

check() {
  cd $pkgname-$pkgver
  # https://github.com/aria2/aria2/issues/1476
  # Upstream states "I don't see any issues with aria2 code."
  make check || echo "Ignoring test failures"
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install

  # add bash completion
  install -d "$pkgdir"/usr/local/share/bash-completion/completions
  install -m644 "$pkgdir"/usr/local/share/doc/aria2/bash_completion/aria2c \
    "$pkgdir"/usr/local/share/bash-completion/completions
  rm -rf "$pkgdir"/usr/local/share/doc/aria2/bash_completion
}
