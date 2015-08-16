# Maintainer: archtux <antonio dot arias99999 at gmail dot com>

pkgname=iichantra
pkgver=1.2
pkgrel=6
pkgdesc="2D jump'n run sidescroller game in a similar style like the original Contra games"
arch=('i686' 'x86_64')
url="http://iichantra.ru/"
license=('MIT')
depends=('devil' 'libbass' 'lua51' 'sdl_net' 'zziplib')
makedepends=('cmake')
options=('!strip')
install=$pkgname.install
source=(http://iichantra.ru/files/pear-dso-src$pkgver.zip
        iichantra
        iichantra.desktop
        iichantra.install
        iichantra.png)
md5sums=('05811dcf2d72c64380037a35c073843c'
         '939ef54d851f774c5d1d84b058aa1dc6'
         '378c2f809b4422a84034cf0eedd86a8f'
         '27e174f19507e2274db9a2dd62699d0e'
         '4a5682a730e590ae408a0ebdd93182c5')


build() {
   cd $srcdir

   # Use libbass from Arch
   sed -i 's%FIND_LIBRARY(LIBBASS bass_x64 PATHS lib)%%' CMakeLists.txt
   sed -i 's%${LIBBASS}%bass%' CMakeLists.txt
   sed -i 's%src/sound/bass.h%%' CMakeLists.txt
   sed -i 's_${LIBBASS}_LIBBASS_' CMakeLists.txt

   # Build
   cmake . -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INCLUDE_PATH=/usr/include/lua5.1
   make
}

package() {
   mkdir -p $pkgdir/usr/share/iichantra
   cp -r bin/* $pkgdir/usr/share/iichantra

   # Change language from russian -> english (comment next line if you want russian)
   sed -i 's_russian_english_' $pkgdir/usr/share/iichantra/config/default.lua

   # License
   install -Dm644 LICENSE $pkgdir/usr/share/licenses/iichantra/LICENSE
   rm $pkgdir/usr/share/iichantra/LICENSE

   # Start file
   cd $startdir
   install -Dm755 iichantra $pkgdir/usr/bin/iichantra

   # Desktop icon
   install -Dm644 $pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
   install -Dm644 $pkgname.png $pkgdir/usr/share/pixmaps/$pkgname.png

   # Remove unneeded libraries
   cd $pkgdir/usr/share/iichantra
   rm *dll *so
}