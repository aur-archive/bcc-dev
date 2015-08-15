
_gccver=4.6.0

pkgname=bcc-dev
pkgver=1.0.39d
pkgrel=1
pkgdesc="Gaisler BCC cross-compiler for SPARC V8 LEON2 and LEON3 processors"
arch=('i686' 'x86_64')
url="http://www.gaisler.com/index.php/products/operating-systems/bcc"
license=('GPL')
options=('!strip')
conflicts=("bcc")
source=("http://developer.gaisler.net/download/bcc/linux/4.6.0/sparc-elf-${_gccver}-${pkgver}.tar.bz2")

if test "$CARCH" == x86_64; then
  depends=("lib32-glibc" "lib32-zlib")
fi

package() {
  mkdir -p $pkgdir/usr/lib/cross-sparc-unknown-elf
  cp -r $srcdir/sparc-elf-$_gccver/* $pkgdir/usr/lib/cross-sparc-unknown-elf

  msg "Cleaning-up cross compiler tree..."
  rm -rf ${pkgdir}/usr/lib/cross-sparc-unknown-elf/{info,man}

  msg "Creating out-of-path executables..."
  mkdir -p ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/
  rm -f ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/*
  cd ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/
  for bin in ${pkgdir}/usr/lib/cross-sparc-unknown-elf/bin/sparc-elf-*; do
    bbin=`basename "$bin"`;
    ln -s "/usr/lib/cross-sparc-unknown-elf/bin/${bbin}" `echo "$bbin" | sed "s#^sparc-elf-##"`;
  done

  msg "Creating /usr/bin symlinks..."
  mkdir -p $pkgdir/usr/bin
  for bin in ${pkgdir}/usr/lib/cross-sparc-unknown-elf/bin/sparc-elf-*; do
    bbin=`basename "$bin"`;
    ln -s "/usr/lib/cross-sparc-unknown-elf/bin/${bbin}" "${pkgdir}/usr/bin/${bbin}";
  done
}

md5sums=('defccd0f3d17d5e7b241ce46a2992e76')

# vim: set ts=2 sw=2 ft=sh noet:
