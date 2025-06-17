# Maintainer: Dz99 <shining.sun0526@gmail.com>
# Contributor: Nick Black <dankamongmen@gmail.com>

pkgname="savvycan"
pkgproper="SavvyCAN"
pkgver="V220"
pkgrel=1
epoch=1
pkgdesc="QT-based CAN bus analysis tool"
url="https://github.com/collin80/SavvyCAN"
license=('MIT')
arch=('x86_64')
depends=('qt5-serialbus' 'qt5-serialport')
makedepends=('qt5-base' 'qt5-tools' 'qt5-declarative')
optdepends=('qt5-clx000-git: clx000 loggers')
source=("https://github.com/collin80/SavvyCAN/archive/refs/tags/${pkgver}.tar.gz")
sha256sums=('1fd00dd3d685810484e87999be65e9e81e5922a6da7f17f3d6d756452b5847bf')
dirvername="${pkgver#V}"

build() {
  cd "$srcdir/$pkgproper-$dirvername"
  sed -i -e '/.*isEmpty(PREFIX)/,+3d' SavvyCAN.pro
  qmake-qt5 PREFIX=/usr \
    QMAKE_CFLAGS="${CFLAGS}" \
    QMAKE_CXXFLAGS="${CXXFLAGS}" \
    QMAKE_LFLAGS="${LDFLAGS}"
  make
}

check() {
  cd "$srcdir/$pkgproper-$dirvername"
  make check
}

package() {
  cd "$srcdir/$pkgproper-$dirvername"
  make INSTALL_ROOT="$pkgdir" install
  qmake-qt5 -install qinstall -exe SavvyCAN "$pkgdir/usr/bin/SavvyCAN"
}

