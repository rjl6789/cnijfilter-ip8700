# Maintainer: rjl6789
#
# Based on:
# cnikfilter-e400series by Kaan Karaagacli <kaankaraagacli@gmail.com>
# cnijfilter2-mg7500 by Yuto Tokunaga (yuntan_t) <toku DOT yuuto AT gmail DOT com>
# cnijfilter-mg3500series by yaroslav <proninyaroslav@mail.ru>
#

pkgname=cnijfilter-ip8700series
pkgver=4.10
pkgrel=1
pkgdesc="Canon IJ Printer Driver (for ip8700 series)"
arch=('i686' 'x86_64')
url="https://www.canon.co.uk/support/consumer_products/products/printers/inkjet/pixma_ip_series/pixma_ip8750.aspx?type=drivers&language=EN&os=Linux%20(64-bit)"
license=('custom')
depends=('popt' 'libcups' 'libxml2')
source=('http://gdlp01.c-wss.com/gds/1/0100005861/01/cnijfilter-ip8700series-4.10-1-deb.tar.gz')
md5sums=('803d5dcd1b7d582096afe90ce6f68de2')

package() {
    if [ "${CARCH}" = 'x86_64' ]; then
      debarch="amd64"
    elif [ "${CARCH}" = 'i686' ]; then
      debarch="i386"
    fi

    cd "$pkgdir"

    # Common files
    ar -x "$srcdir/${pkgname}-${pkgver}-1-deb/packages/cnijfilter-common_${pkgver}-1_${debarch}.deb" data.tar.gz
    tar -xf data.tar.gz && rm data.tar.gz

    # Model specific files
    ar -x "$srcdir/${pkgname}-${pkgver}-1-deb/packages/${pkgname}_${pkgver}-1_${debarch}.deb" data.tar.gz
    tar -xf data.tar.gz && rm data.tar.gz

    # Weird permissions error from namcap
    chmod 664 usr/lib/bjlib/cnnet.ini
    chown root:root usr/lib/bjlib/cnnet.ini

    # Move licenses to their proper locations
    install -d usr/share/licenses/cnijfilter-ip8700series
    mv usr/share/doc/cnijfilter-common/LICENSE-cnijfilter-${pkgver}*.txt usr/share/licenses/${pkgname}/
    rm -r usr/share/doc/

    # Move the udev rule to its proper location
    mv etc/udev usr/lib/
    rmdir etc/
}
