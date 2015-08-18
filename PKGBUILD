# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=yap-git
pkgver=6548.66af6f7
pkgrel=1
pkgdesc='An high-performance Prolog compiler (Development version)'
url='http://www.dcc.fc.up.pt/~vsc/Yap/'
license=('PerlArtistic' 'LGPL2.1')
arch=('i686' 'x86_64')
depends=('unixodbc' 'libmariadbclient')
optdepends=('java-runtime-headless: Java Interface Library JPL'
            'mpe2: MPE interface'
            'mpich: MPICH based MPI interface'
            'lam: MPI LAM-based interface')
makedepends=('texi2html')
provides=('yap')
conflicts=('yap')
source=(yap::git://yap.git.sourceforge.net/gitroot/yap/yap-6.3)
md5sums=('SKIP')

pkgver() {
  cd yap
  echo $(git rev-list --count master).$(git rev-parse --short master)
}

build() {
  cd yap

  git submodule init
  git submodule update

  ./configure \
    --prefix=/usr \
    --with-java="${JAVA_HOME}" \
    --enable-max-performance \
    --enable-max-memory \
    --enable-dynamic-loading
  make

  # Build docs
  make pdf
  make html
}

package() {
  cd yap
  make DESTDIR="${pkgdir}" install
  make DESTDIR="${pkgdir}" install_docs
}
