# Maintainer: rubenvb vanboxem <dottie> ruben <attie> gmail <dottie> com
pkgname=mingw-w64-crt-svn
pkgver=6362
pkgrel=1
pkgdesc='MinGW-w64 CRT for Windows'
arch=('any')
url='http://mingw-w64.sourceforge.net'
license=('custom')
groups=('mingw-w64-toolchain' 'mingw-w64')
depends=('mingw-w64-gcc-base' 'mingw-w64-binutils' 'mingw-w64-headers-svn' 'mingw-w64-headers-bootstrap')
makedepends=('svn')
optdepends=()
provides=('mingw-w64-crt')
conflicts=('mingw-w64-crt')
replaces=()
backup=()
options=('!strip' 'staticlibs' 'staticlibs' '!emptydirs')
source=(svn+svn://svn.code.sf.net/p/mingw-w64/code/trunk/mingw-w64-crt)
md5sums=(SKIP)

_targets="i686-w64-mingw32 x86_64-w64-mingw32"

pkgver() {
  cd "$SRCDEST/mingw-w64-crt"
  svnversion
}

build() {
  for _target in ${_targets}; do
    msg "Building ${_target} CRT"
    if [ ${_target} == "i686-w64-mingw32" ]; then
        _crt_configure_args="--disable-lib64 --enable-lib32"
    elif [ ${_target} == "x86_64-w64-mingw32" ]; then
        _crt_configure_args="--disable-lib32 --enable-lib64"
    fi
    mkdir -p ${srcdir}/crt-${_target} && cd ${srcdir}/crt-${_target}
    ${srcdir}/mingw-w64-crt/configure --prefix=/usr/${_target} \
        --host=${_target} --enable-wildcard \
        ${_crt_configure_args}
    make
  done
}

package() {
  for _target in ${_targets}; do
    msg "Installing ${_target} crt"
    cd ${srcdir}/crt-${_target}
    make DESTDIR=${pkgdir} install
  done
}

