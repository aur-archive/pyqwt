# Maintainer: Andrzej Giniewicz <gginiu@gmail.com>
# Contributor:  Eugen Zagorodniy <e dot zagorodniy at gmail dot com>
# Contributor: Olaf Leidinger <leidola@newcon.de>
# Contributer: Henning Garus <henning.garus@gmail.com>
# Contributor: Thomas Burdick <thomas.burdick@gmail.com>

pkgname=pyqwt
pkgver=5.2.0
pkgrel=12
pkgdesc="Python bindings for Qt Widgets for Technical Applications"
arch=("i686" "x86_64")
url="http://pyqwt.sourceforge.net/"
depends=('python2' 'python2-pyqt>=4.6.0' 'python2-pyqt<4.10' 'python2-numpy>=1.1.0' 'qwt5>=5.0.2' 'sip>=4.7.6' 'sip<5')
options=('!makeflags')
license=("GPL")
source=("http://downloads.sourceforge.net/sourceforge/pyqwt/PyQwt-$pkgver.tar.gz"
        "qplt.py-r1.21.patch" "configure.patch"
)
md5sums=('fcd6c6029090d473dcc9df497516eae7'
         '30011f9139ad12ddbeac79c6a45d4b43'
         'd1f2c673321f85dccc5207708f5c8c6b')

build() {
  cd "$srcdir"/PyQwt-$pkgver

  patch -p1 < ../qplt.py-r1.21.patch
  patch -p1 < ../configure.patch

  cd configure
  python2 configure.py -I/usr/include/qwt5 -lqwt5 --extra-include-dirs=/usr/include/qt4
  sed -i "s|/usr/include/Qt|/usr/include/qt4/Qt|g" iqt5qt4/Makefile
  sed -i "s|/usr/include/Qt|/usr/include/qt4/Qt|g" qwt5qt4/Makefile
  make
}

package() {
  cd "$srcdir"/PyQwt-$pkgver/configure

  make DESTDIR="$pkgdir" install

  sed -i -e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2|" $(find "${pkgdir}" -name '*.py')
}

