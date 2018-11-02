# Maintainer: eolianoe <eolianoe [at] gmail [DoT] com>
pkgname=${MINGW_PACKAGE_PREFIX}-coin-or-ipopt
pkgver=3.12.11
pkgrel=1
pkgdesc="Interior Point OPTimizer"
arch=('any')
url="https://projects.coin-or.org/Ipopt"
license=('EPL')
depends=("${MINGW_PACKAGE_PREFIX}-openblas" "${MINGW_PACKAGE_PREFIX}-gcc-libs" "${MINGW_PACKAGE_PREFIX}-gcc-libgfortran")
makedepends=("${MINGW_PACKAGE_PREFIX}-gcc-fortran" "wget")
source=("http://www.coin-or.org/download/source/Ipopt/Ipopt-$pkgver.tgz")
sha1sums=('cede6497ec8b4c3ccb96256d6430a39ea353af69')

prepare(){
  cd "$srcdir/Ipopt-$pkgver/ThirdParty/ASL" && ./get.ASL
  cd "$srcdir/Ipopt-$pkgver/ThirdParty/Metis" && ./get.Metis
  cd "$srcdir/Ipopt-$pkgver/ThirdParty/Mumps" && ./get.Mumps
}

build() {
  cd "$srcdir"
  mkdir -p build && pushd build
  "$srcdir/Ipopt-$pkgver/./configure" \
                                      --prefix=${MINGW_PREFIX} --with-blas="-L${MINGW_PREFIX}/lib -lopenblas" \
                                      --with-lapack="-L${MINGW_PREFIX}/lib -lopenblas" \
                                      ADD_CFLAGS="-fopenmp --static" \
                                      ADD_FFLAGS="-fopenmp --static" \
                                      ADD_CXXFLAGS="-fopenmp --static"
  make
}

check() {
  cd "$srcdir/build"
  #make tests
}

package() {
  cd "$srcdir/build"
  PKG_CONFIG_LIBDIR="${pkgdir}${MINGW_PREFIX}/lib/pkgconfig/" \
  make DESTDIR="$pkgdir/" PREFIX="${MINGW_PREFIX}" install
}

