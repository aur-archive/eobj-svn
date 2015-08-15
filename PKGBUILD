export CFLAGS="${CFLAGS} -g"
# $Id: PKGBUILD 76272 2012-09-15 10:07:18Z rvanharen $
# Maintainer: Ronald van Haren <ronald.archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>

pkgname=eobj-svn
pkgver=78409
pkgrel=1
pkgdesc="EO description"
arch=('i686' 'x86_64')
groups=('e17-libs-svn' 'e17-svn')
url="http://www.enlightenment.org"
license=('BSD')
depends=('libxp' 'curl' 'libxss' 'evas-svn' 'libxtst' 'libxcomposite' 
	'libxrandr' 'libxinerama' 'libxcursor' 'eina-svn')
makedepends=('subversion')
provides=('eobj' 'eo')
options=('!libtool' '!emptydirs')
source=()
md5sums=()

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/PROTO/eobj"
_svnmod="eobj"

build() {
  cd $srcdir

  if [ $NOEXTRACT -eq 0 ]; then
    msg "Connecting to $_svntrunk SVN server...."
    if [ -d $_svnmod/.svn ]; then
      (cd $_svnmod && svn up -r $pkgver)
    else
      svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
    fi

    msg "SVN checkout done or server timeout"
    msg "Starting make..."

  fi
  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build
  ./autogen.sh --prefix=/usr \

  make
}

package(){
  cd $srcdir/$_svnmod-build
  make DESTDIR=$pkgdir install
 
# install license files
  install -Dm644 $srcdir/$_svnmod-build/COPYING \
        $pkgdir/usr/share/licenses/$pkgname/COPYING
 
  rm -r $srcdir/$_svnmod-build

}
