# $Id: PKGBUILD 165226 2012-08-13 20:41:20Z eric $
# Jubei-Mitsuyoshi <jubei.house.of.five.masters@gmail.com>
# Contributor: Ivailo Monev <xakepa10@gmail.com>

pkgname=('device-mapper-lsd')
_axepkgname=('device-mapper')
pkgver=2.03.97
_axepkgver=2.02.97
pkgrel=2
groups=('base' 'lsd')
arch=('i686' 'x86_64')
pkgdesc="Device mapper userspace library and tools -lsd version without systemd support"
url="http://sourceware.org/dm/"
license=('GPL2' 'LGPL2.1')
depends=('glibc' 'udev')
provides=("device-mapper=$pkgver")
conflicts=("device-mapper<$pkgver")
source=(ftp://sources.redhat.com/pub/lvm2/LVM2.${_axepkgver}.tgz{,.asc}
        11-dm-initramfs.rules)
sha1sums=('ca92d976628246745f0981d1514a79a4a8e32314'
          '9f0c6047fe3c275db7af20f383bd41744fcafc33'
          'f6a554eea9557c3c236df2943bb6e7e723945c41')

build() {
  cd "${srcdir}/LVM2.${_axepkgver}"
  unset LDFLAGS

  ./configure --prefix=/ --sbindir=/sbin --sysconfdir=/etc --localstatedir=/var --datarootdir=/usr/share \
    --includedir=/usr/include --with-usrlibdir=/usr/lib  --libdir=/usr/lib --with-udev-prefix=/usr \
    --enable-dmeventd --enable-cmdlib --enable-applib --enable-udev_sync --enable-udev_rules  \
    --with-default-locking-dir=/run/lock/lvm
  make
}

#removed by axe cos we dont want sysd
#  --with-systemdsystemunitdir=/usr/lib/systemd/system --enable-pkgconfig --enable-readline 

package() {
  cd "${srcdir}/LVM2.${_axepkgver}"
  make DESTDIR="${pkgdir}" install_device-mapper
  # extra udev rule for device-mapper in initramfs
  install -D -m644 "${srcdir}/11-dm-initramfs.rules" "${pkgdir}/usr/lib/initcpio/udev/11-dm-initramfs.rules"
}
