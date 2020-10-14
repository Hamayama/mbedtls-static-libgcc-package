# Maintainer: Nazar Mishturak <nazar m x at gmail dot com>
# Modification: Hamayama <fkyo0985@gmail.com>

PKGEXT='.pkg.tar.xz'
_realname=mbedtls
pkgbase="mingw-w64-${_realname}-static-libgcc"
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}-static-libgcc"
pkgver=2.16.5
pkgrel=1
arch=('any')
url='https://tls.mbed.org/'
pkgdesc='mbed TLS is an open source and commercial SSL library licensed by ARM Limited. (mingw-w64) (build with -static-libgcc)'
depends=("${MINGW_PACKAGE_PREFIX}-gcc-libs")
makedepends=("${MINGW_PACKAGE_PREFIX}-gcc"
             #"${MINGW_PACKAGE_PREFIX}-cmake"
             #"${MINGW_PACKAGE_PREFIX}-doxygen"
             #"${MINGW_PACKAGE_PREFIX}-graphviz"
             )
license=('Apache License 2.0')
options=('strip' 'staticlibs' 'docs')
source=(${_realname}-${pkgver}.tar.gz::"https://tls.mbed.org/download/mbedtls-${pkgver}-apache.tgz"
        'symlink-test.patch'
        'dll-location.patch'
        'enable-features.patch')
sha256sums=('65b4c6cec83e048fd1c675e9a29a394ea30ad0371d37b5742453f74084e7b04d'
            'd6aa304dbad652da2b1ee8eaf29422309b72633e1b33fe4bb67fc21b529d3bb5'
            '89eb82f9e9fb456d0595035925d2d512aa2ca9b9e283b9c51d5524bfc8dbf996'
            '1be88267b045a8728fe4dde663faf328ad788eeefcb43915beeb364b4d2dd2e8')
conflicts=(${MINGW_PACKAGE_PREFIX}-${_realname})

prepare() {
  cd "${srcdir}/${_realname}-${pkgver}"
  patch -p1 -i "${srcdir}/symlink-test.patch"
  patch -p1 -i "${srcdir}/dll-location.patch"
  patch -p1 -i "${srcdir}/enable-features.patch"
}

build() {
  cd "${srcdir}/${_realname}-${pkgver}"

  local BUILD_TYPE="Release"
  if check_option "debug" "y"; then
    BUILD_TYPE="Debug"
  fi
  
  [[ -d ${srcdir}/build-${MINGW_CHOST} ]] && rm -rf ${srcdir}/build-${MINGW_CHOST}
  mkdir -p ${srcdir}/build-${MINGW_CHOST}
  cd ${srcdir}/build-${MINGW_CHOST}
  
  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
  #${MINGW_PREFIX}/bin/cmake \
  cmake \
    -G"MSYS Makefiles" \
    -DCMAKE_BUILD_TYPE=${BUILD_TYPE} \
    -DCMAKE_INSTALL_PREFIX=${MINGW_PREFIX} \
    -DCMAKE_C_COMPILER=${MINGW_CHOST}-gcc \
    -DENABLE_TESTING=ON \
    -DENABLE_PROGRAMS=OFF \
    -DUSE_SHARED_MBEDTLS_LIBRARY=ON \
    -DUSE_STATIC_MBEDTLS_LIBRARY=ON \
    -DCMAKE_SHARED_LINKER_FLAGS="-static-libgcc" \
    ../${_realname}-${pkgver}
  make
  # Generate the documentation
  #make apidoc
}

check() {
  cd "${srcdir}/build-${MINGW_CHOST}"
  cp -p library/*.dll tests/ # Tests are dynamically linked
  make test
}

package () {
  cd "${srcdir}/build-${MINGW_CHOST}"
  make DESTDIR=${pkgdir} install
  
  # Install the documentation
  cd "${srcdir}/${_realname}-${pkgver}"
  #mkdir -p "${pkgdir}/${MINGW_PREFIX}/share/doc/${_realname}"
  #cp -Rp apidoc "${pkgdir}/${MINGW_PREFIX}/share/doc/${_realname}/html"
}
