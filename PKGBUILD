# Contributor: Feufochmar <feufochmar.gd@gmail.com>
pkgname=fvkbd-git
pkgver=20130221
pkgrel=1
pkgdesc="A free and flexible Virtual Keyboard aiming at providing fancy UI and easy to config layout"
arch=('i686' 'x86_64')
url="http://gitorious.org/fvkbd/pages/Home"
license=('LGPL')
depends=('gtk2' 'libxml2' 'libfakekey' 'libunique')
makedepends=('git')
optdepends=('python-dbus')
 
_gitroot="git://gitorious.org/fvkbd/fvkbd.git"
_gitname="fvkbd"
 
build() {
  cd $srcdir
  msg "Connecting to the GIT server...."
  
  if [[ -d $srcdir/$_gitname ]] ; then
    cd $_gitname
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi
  
  msg "GIT checkout done"
  msg "Starting make..."
  
  cd $srcdir/$_gitname
 
  # remove the -Werror flag as there are some variables unused
  find * -name "Makefile.am" | xargs grep -l Werror | xargs sed -i s/-Werror//g
 
  ./autogen.sh
  ./configure --prefix=/usr --sysconfdir=/etc
  
  make
}
 
package() {
  cd $srcdir/$_gitname
  make DESTDIR=$pkgdir install
}
