# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm.desktop
	dwm-activetagindicatorbar-6.2.diff
	dwm-alternativetags-6.2.diff
	dwm-fullgaps-6.2.diff
	dwm-restartsig-20180523-6.2.diff)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            '06e5b1c6b339fc511bb7875dc6c5d8aa1f29fef2e86a94d8fb01bfff0d5e3078'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81'
            '54aa85bd1e2ef90eb26be3ea68502eb987c865be22dd53768014c46f9eb88720'
            '6a8cda675210014ab169caa0e78119ad95a5ed1dfb3a464a8a970001e86a1814'
            '3c59104f4b23b8ec3c31ff639712dc1214bd5e3a487f7af039268373eb9e0b2d'
            'c74f2f41da552b0c8629ddb9fec7b40a035581041cf198d81a43d4b16b742f69')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  patch --forward --strip=1 --input="${srcdir}/dwm-fullgaps-6.2.diff"
  patch --forward --strip=1 --input="${srcdir}/dwm-activetagindicatorbar-6.2.diff"
  patch --forward --strip=1 --input="${srcdir}/dwm-alternativetags-6.2.diff"
  patch --forward --strip=1 --input="${srcdir}/dwm-restartsig-20180523-6.2.diff"
  cp "$srcdir/config.h" config.h
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
