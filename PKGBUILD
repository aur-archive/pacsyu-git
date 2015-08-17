# Maintainer: Alfonso Saavedra "Son Link" <sonlink.dourden@gmail.com>
pkgname=pacsyu-git
_pkgname=pacsyu
pkgver=20120116
pkgrel=1
pkgdesc="Update notifier based on python2 and GTK2"
arch=(any)
url="http://sonlinkblog.blogspot.com/p/pacsyu.html"
license=('GPL3')
groups=()
depends=('vte' 'python2' 'pygtk' 'python-notify' 'sudo' 'cower')
makedepends=('git')
source=('pacsyu.desktop' 'sample.pacsyu')
md5sums=('b778fd770f657ff517315e73a7f18081'
         '2cdb4521a959592f3614cd8b1b30333b')

_gitroot="git://github.com/son-link/PacSyu.git"
_gitname="PacSyu"

build() {
  msg "Connecting to GIT server...."

 if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
}
package() {
  cd "${srcdir}/${_gitname}"
  msg "Starting make..."

  mkdir -p $pkgdir/usr/share/$_pkgname
  mkdir -p $pkgdir/usr/bin
  mkdir -p $pkgdir/usr/share/locale
	
  install -m755 $_pkgname.py $pkgdir/usr/bin/$_pkgname
  sed -i "s/lang/\/usr\/share\/locale/g" $pkgdir/usr/bin/$_pkgname
  sed -i "s/modules/\/usr\/share\/$_pkgname/g" $pkgdir/usr/bin/$_pkgname
  sed -i "s/COPYING/\/usr\/share\/$_pkgname\/COPYING/g" $pkgdir/usr/bin/$_pkgname

  cp modules/* *.svg COPYING CHANGELOG README $pkgdir/usr/share/$_pkgname/
  
  mkdir -p $pkgdir/usr/share/icons/
  cp pacsyu.svg $pkgdir/usr/share/icons/
  
  sed -i "s/copyfile('/copyfile('\/usr\/share\/$_pkgname\//g" $pkgdir/usr/share/$_pkgname/config.py
  sed -i "s/gtk.gdk.pixbuf_new_from_file('/gtk.gdk.pixbuf_new_from_file('\/usr\/share\/icons\//g" $pkgdir/usr/bin/$_pkgname

  cp lang/* -r $pkgdir/usr/share/locale/
  
  mkdir -p $pkgdir/usr/share/applications/
  install -Dm644 "${srcdir}/pacsyu.desktop" "${pkgdir}/usr/share/applications/pacsyu.desktop"
  install -Dm644 "${srcdir}/sample.pacsyu" "${pkgdir}/usr/share/$_pkgname/sample.$_pkgname"
	
}
