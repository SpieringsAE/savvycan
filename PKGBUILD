# Maintainer: Maud Spierings <maud_spierings@murena.io>
# Contributor: Dz99 <shining.sun0526@gmail.com>
# Contributor: Nick Black <dankamongmen@gmail.com>

pkgname="savvycan"
_pkgproper="SavvyCAN"
pkgver="V220"
pkgrel=1
epoch=1
pkgdesc="QT-based CAN bus analysis tool"
url="https://github.com/collin80/SavvyCAN"
license=('MIT')
arch=('x86_64' 'aarch64' 'riscv64')
depends=('libglvnd' 'glibc' 'gcc-libs' 'qt5-base' 'qt5-serialbus' 'qt5-serialport' 'qt5-declarative' 'hicolor-icon-theme')
makedepends=('qt5-tools')
optdepends=('qt5-clx000-git: clx000 loggers' 'qt5-wayland: wayland APIs')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/collin80/SavvyCAN/archive/refs/tags/${pkgver}.tar.gz")
sha256sums=('1fd00dd3d685810484e87999be65e9e81e5922a6da7f17f3d6d756452b5847bf')
_dirvername="${pkgver#V}"

build() {
  cd "$srcdir/$_pkgproper-$_dirvername"
  sed -i -e '/.*isEmpty(PREFIX)/,+3d' SavvyCAN.pro
  qmake-qt5 PREFIX=/usr \
    QMAKE_CFLAGS="${CFLAGS}" \
    QMAKE_CXXFLAGS="${CXXFLAGS}" \
    QMAKE_LFLAGS="${LDFLAGS}"
  make
}

check() {
  cd "$srcdir/$_pkgproper-$_dirvername"
  make check
}

package() {
  cd "$srcdir/$_pkgproper-$_dirvername"
  make INSTALL_ROOT="$pkgdir" install
  qmake-qt5 -install qinstall -exe SavvyCAN "$pkgdir/usr/bin/SavvyCAN"
  install -dm755 "$pkgdir/usr/share/licenses/$pkgname/"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/"
}

