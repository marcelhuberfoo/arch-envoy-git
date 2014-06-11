# Maintainer: Simon Gomizelj <simongmzlj@gmail.com>
# Contributor: Marcel Huber <`echo "moc tknup liamg tä oofrebuhlecram" | rev`>

pkgname=envoy-git
pkgver=8.25.g7c667a6
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
source=("$pkgname"::'git+git://github.com/vodik/envoy.git')
sha1sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  if GITTAG="$(git describe --abbrev=0 --tags 2>/dev/null)"; then
    local _revs_ahead_tag=$(git rev-list --count ${GITTAG}..)
    local _commit_id_short=$(git log -1 --format=%h)
    echo $(sed -e s/^${pkgname%%-git}// -e 's/^[-_/a-zA-Z]\+//' -e 's/[-_+]/./g' <<< ${GITTAG}).${_revs_ahead_tag}.g${_commit_id_short}
  else
    echo 0.$(git rev-list --count master).g$(git log -1 --format=%h)
  fi
}

prepare() {
  cd "$srcdir/$pkgname"
}

build() {
  cd "$srcdir/$pkgname"
  make
}

package() {
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir" install
  mkdir "$pkgdir/usr/lib/systemd/user"
  cd "$pkgdir/usr/lib/systemd/user"
  ln -s "$pkdir/usr/lib/systemd/system/envoy@.service" "$pkdir/usr/lib/systemd/system/envoy@.socket" .
}

# vim: set ft=sh syn=sh ts=2 sw=2 et:
