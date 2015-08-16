# First maintainer: Jan Böhringer <janboe@gmail.com>
# Forked maintainer GI_Jack<GI_Jack@hushmail.com>

#modified packagebuild found on AUR with the following.
# added kernel crypto support
# added mcrypt support
# added plugins for nautilus(gnome) and thunar(xfce) file managers

pkgbase=gtkhash
pkgname=gtkhash-thunar-enabled
pkgver=0.6.0
pkgrel=1
pkgdesc="A GTK+ utility for computing message digests or checksums.(with filemanager plugins)"
arch=('i686' 'x86_64' 'mips64el')
url="http://gtkhash.sourceforge.net/"
license=('GPL')
depends=('gtk2' 'mhash' 'gconf' 'intltool' 'thunar')
optdepends=('libgcrypt' 'zlib')
source=(http://downloads.sourceforge.net/$pkgbase/$pkgbase-$pkgver.tar.gz
	gtkhash.desktop)

build() {
  cd $startdir/src/$pkgbase-$pkgver
  ./configure --enable-linux-crypto --enable-thunar --prefix=/usr || return 1
  make || return 1
  make DESTDIR=$startdir/pkg install || return 1
  install -m755 -d "${pkgdir}/usr/share/gconf/schemas"
  gconf-merge-schema "${pkgdir}/usr/share/gconf/schemas/${pkgbase}.schemas" --domain $pkgbase ${pkgdir}/usr/etc/gconf/schemas/*.schemas || return 1
  rm -rf ${pkgdir}/usr/etc/
  install -D -m644 $startdir/src/gtkhash.desktop $startdir/pkg/usr/share/applications/gtkhash.desktop || return 1 
}

md5sums=('71980923ccf6d11715b1d2bfc7a5dfc6'
         'baaf96833613fdc5ded1cf8e1972ba3f')
