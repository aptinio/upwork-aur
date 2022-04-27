# Maintainer: Yurii Kolesnykov <root@yurikoles.com>

pkgname=upwork
pkgver=5.6.10.1
_hashver='de501d28cc034306'
_pkgname='Upwork'
pkgrel=1
pkgdesc='Upwork Desktop Application'
arch=(x86_64)
url='https://www.upwork.com/ab/downloads/os/linux/'
license=(custom)
depends=(alsa-lib gtk3 libxss nss)
source=(https://upwork-usw2-desktopapp.upwork.com/binaries/v${pkgver//./_}_${_hashver}/upwork_${pkgver}_amd64.deb
        LICENSE)
sha256sums=('8faf896d2570d1d210793f46a3860e934d03498c1f11640d43721b6eb2b56860'
            '793d8d7bc0f088c48798bda3d5483972636c6b8c5dcd9aeaf85411f7d4547b38')

prepare() {
    bsdtar -xpf data.tar.xz
}

package() {
    # Base
    install -dm755 $pkgdir/opt/${_pkgname}
    cp -dr --no-preserve=ownership opt/${_pkgname}/* $pkgdir/opt/${_pkgname}/

    # Code ref: https://github.com/electron-userland/electron-builder/blob/master/packages/app-builder-lib/templates/linux/after-install.tpl
    # SUID chrome-sandbox for Electron 5+
    test -e $pkgdir/opt/${_pkgname}/chrome-sandbox && chmod 4755 $pkgdir/opt/${_pkgname}/chrome-sandbox || true

    # Exec
    install -dm755 $pkgdir/usr/bin/
    ln -s /opt/${_pkgname}/${pkgname} $pkgdir/usr/bin/

    # Menu
    install -Dm644 usr/share/applications/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop

    # Icons
    install -dm755 $pkgdir/usr/share
    cp -dr --no-preserve=ownership usr/share/icons "${pkgdir}/usr/share"

    # License
    install -Dm644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
