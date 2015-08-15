# Maintainer: Brian Bidulock <bidulock@openss7.org>
# Contributor: Ryan Corder <ryanc@greengrey.org>
# Contributor: Samuel Tardieu <sam@rfc1149.net>
pkgname=ckermit
pkgver=9.0.302
pkgrel=5
pkgdesc="Portable scriptable network and serial communication software"
arch=('i686' 'x86_64')
license=('custom')
depends=('ncurses')
source=('ftp://kermit.columbia.edu/kermit/archives/cku302.tar.gz' 'lockdir.patch')
source=('ftp://ftp.kermitproject.org/kermit/archives/cku302.tar.gz' 'lockdir.patch')
url="http://www.columbia.edu/kermit/ck90.html"
md5sums=('eac4dbf18b45775e4cdee5a7c74762b0'
         '5968e55dd472b2efb0e31cb3a6fb1655')

build() {
    cd $srcdir
    chmod -R og-rwx ./
    patch -p1 < lockdir.patch

    make linux || return 1
}
package() {
    cd $srcdir

    mkdir -m 0755 -p $pkgdir/usr/bin || return 1
    mkdir -m 0755 -p $pkgdir/usr/share/man/man1 || return 1
    mkdir -m 0755 -p $pkgdir/usr/share/licenses/$pkgname || return 1

    install -m 755 wermit $pkgdir/usr/bin/ckermit || return 1
    ln -s /usr/bin/ckermit $pkgdir/usr/bin/ckermit-sshsub
    install -m 644 ckuker.nr $pkgdir/usr//share/man/man1/ckermit.1 || return 1
    install -m 644 COPYING.TXT $pkgdir/usr/share/licenses/$pkgname/License.txt || return 1

    echo "#!/usr/bin/ckermit" > _tmp.ini
    cat ckermit.ini >> _tmp.ini
    install -m 755 _tmp.ini $pkgdir/usr/bin/ckermit.ini
}
