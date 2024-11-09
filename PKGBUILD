# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=importlib-metadata
_Pkg=importlib_metadata
pkgname="${_py}-${_pkg}"
pkgver=5.0.0
_commit=009ace37032742922d5fa04c62f04cea703ade2d
pkgrel=5
pkgdesc="Read metadata from Python packages"
url="https://${_pkg}.readthedocs.io"
license=(
  'Apache'
)
arch=(
  'any'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-zipp"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools-scm"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pyfakefs"
  "${_py}-pip"
  "${_py}-tests"
)
_http="https://github.com"
_ns="python"
_url="${_http}/${_ns}/${_Pkg}"
source=(
  "${_pkg}::git+${_url}.git#commit=${_commit}"
)
sha512sums=(
  'SKIP'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    -nw
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      pytest \
    --ignore \
    "exercises.py"
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="$pkgdir" \
    dist/*.whl
}
