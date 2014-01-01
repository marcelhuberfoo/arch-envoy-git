# Maintainer: Simon Gomizelj <simongmzlj@gmail.com>

pkgname=envoy-git
pkgver=7.8.gf510efd
pkgver() {
  cd "envoy"
  git describe | sed 's/^v//;s/-/./g'
}
pkgrel=1
pkgdesc="A ssh-agent/gpg-agent keychain and process monitor"

arch=('i686' 'x86_64')
url="http://github.com/vodik/envoy"
license=('GPL')
depends=('openssh' 'systemd')
optdepends=('gnupg: gpg-agent support')
makedepends=('git' 'ragel')
conflicts=('envoy')
provides=('envoy')
source=('git+git://github.com/vodik/envoy.git'
        'git+git://github.com/vodik/clique.git')
sha1sums=('SKIP' 'SKIP')

prepare() {
  cd "envoy"

  # workaround for submodules
  git submodule init
  git config submodule.clique.url "$srcdir/clique"
  git submodule update
}

build() {
  make -C "envoy"
}

package() {
  make -C "envoy" DESTDIR="$pkgdir" install

  mkdir "$pkgdir/usr/lib/systemd/user"
  cd "$pkgdir/usr/lib/systemd/user"
  ln -s "$pkdir/usr/lib/systemd/system/envoy@.service" "$pkdir/usr/lib/systemd/system/envoy@.socket" .
}

# vim: ft=sh syn=sh et
