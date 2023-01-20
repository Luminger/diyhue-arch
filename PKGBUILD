# Maintainer: Simon Brakhane <simon+packages@brakhane.net>
pkgname=diyHue
pkgver=2022.8
pkgrel=1
epoch=
pkgdesc='A Hue Bridge Emulator'
arch=('x86_64' 'aarch64' 'armv7h')
url='https://github.com/diyhue/diyHue'
license=('custom')
groups=()
depends=('openssl' 'nmap' 'curl' 'python' 'python-astral' 'python-ws4py'
         'python-requests' 'python-paho-mqtt' 'python-email-validator'
         'python-flask' 'python-flask-cors' 'python-flask-login'
         'python-flask-restful' 'python-flask-wtf' 'python-yaml'
         'python-zeroconf' 'libcoap')
makedepends=()
checkdepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=("https://github.com/diyHue/diyHue/archive/refs/tags/$pkgver.tar.gz"
        "https://github.com/diyhue/diyHueUI/releases/download/v1.0.0/DiyHueUI-release.zip"
        'remove-protocols.patch')
sha256sums=('368d98432539eb22760e877d9fac50df1ae2ea39feb5f07c981873f69fc8dc0b'
            '5271580a28ee2be78d7df0206eda97a67354fbef25cf78202f229c0c9d76b58d'
            '38dfac038269680b12befe61d9704b4fb154db6d03448de9b48c3a391166280f')
noextract=()
validpgpkeys=()

prepare() {
    patch --forward --strip=1 --input="${srcdir}/remove-protocols.patch"
}

package() {
	cd "$pkgname-$pkgver"

    mkdir -p $pkgdir/opt/hue-emulator/
    cp -r BridgeEmulator/flaskUI/ \
          BridgeEmulator/functions/ \
          BridgeEmulator/lights/ \
          BridgeEmulator/sensors/ \
          BridgeEmulator/HueObjects/ \
          BridgeEmulator/services/ \
          BridgeEmulator/configManager/ \
          BridgeEmulator/logManager/ $pkgdir/opt/hue-emulator/

    cp BridgeEmulator/openssl.conf \
       BridgeEmulator/HueEmulator3.py \
       BridgeEmulator/genCert.sh $pkgdir/opt/hue-emulator/
    
    ln -s /usr/bin/coap-client $pkgdir/opt/hue-emulator/coap-client-linux

    mkdir $pkgdir/opt/hue-emulator/config/

    mkdir -p $pkgdir/usr/lib/systemd/system/
    cp BridgeEmulator/hue-emulator.service $pkgdir/usr/lib/systemd/system/

    mkdir -p $pkgdir/usr/share/licenses/$pkgname/
    cp LICENSE.md $pkgdir/usr/share/licenses/$pkgname/

    cd ..
    cp index.html $pkgdir/opt/hue-emulator/flaskUI/templates/
    cp -r static $pkgdir/opt/hue-emulator/flaskUI/
}
