# $Id: PKGBUILD 171305 2012-11-17 04:08:09Z stephane $
# Upstream Maintainer: Stéphane Gaudreault <stephane@archlinux.org>
# Contributor: Sebastien Binet <binet@farnsworth>
# Maintainer: Fantix King <fantix.king at gmail.com>
pkgbase=libx32-python-distribute
#pkgname=('python-distribute' 'python2-distribute')
pkgname=libx32-python2-distribute
pkgver=0.6.30
pkgrel=1.1
pkgdesc="Easily build and distribute Python packages (x32 ABI)"
arch=('x86_64')
license=('PSF')
url="http://pypi.python.org/pypi/distribute"
makedepends=('python' 'python2')
makedepends=('binx32-python2')
source=(http://pypi.python.org/packages/source/d/distribute/distribute-${pkgver}.tar.gz
        distribute-python2_and_3.patch)
sha1sums=('40dfce237883d1c02817f726128f61614dc686ff'
          '9c19c12edac507b0f76696d282b9831c4b653a7e')
build() {
   cd "${srcdir}"

   pushd distribute-${pkgver}
   patch -Np1 -i ../distribute-python2_and_3.patch
   popd

   cp -a distribute-${pkgver}{,-python2}

   # Build python 3 module
   cd distribute-${pkgver}

   #sed -i -e "s|^#\!.*/usr/bin/python|#!/usr/bin/python3|" setuptools/tests/test_resources.py

   #python3 setup.py build

   # Build python 2 module
   cd ../distribute-${pkgver}-python2

   sed -i -e "s|^#\!.*/usr/bin/python|#!/usr/bin/python2|" setuptools/tests/test_resources.py

   python2-x32 setup.py build
}

package_python-distribute() {
   depends=('python>=3.3')

   cd "${srcdir}/distribute-${pkgver}"
   python3 setup.py install --prefix=/usr --root="${pkgdir}" --optimize=1 --skip-build
}

package_libx32-python2-distribute() {
   depends=('binx32-python2>=2.7')
   provides=('binx32-setuptools')
   conflicts=('binx32-setuptools')

   cd "${srcdir}/distribute-${pkgver}-python2"
   python2-x32 setup.py install --prefix=/usr --root="${pkgdir}" --optimize=1 --skip-build

   mv "${pkgdir}/usr/bin/easy_install-2.7" "${pkgdir}/usr/bin/easy_install-2.7-x32"
}
