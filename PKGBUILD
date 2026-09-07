pkgname=unidesk
pkgver=1.0
pkgrel=1
pkgdesc="Welcome and academic configuration app for UniOS"
arch=('any')
url="https://github.com/opensource-uom/unidesk"
license=('GPL-3.0-or-later')
depends=(
    'python'
    'python-pyqt6'
)
makedepends=(
    'python-build'
    'python-installer'
    'python-wheel'
    'python-setuptools'
)
source=()
sha256sums=()

build() {
    cd "$startdir"
    python -m build --wheel --no-isolation
}

package() {
    cd "$startdir"

    python -m installer --destdir="$pkgdir" dist/*.whl

    install -d "$pkgdir/usr/share/applications"
    install -d "$pkgdir/etc/xdg/autostart"
    install -d "$pkgdir/usr/share/pixmaps"
    install -d "$pkgdir/usr/share/icons/hicolor/128x128/apps"

    if [ -f "$startdir/resources/unios.png" ]; then
        install -Dm644 "$startdir/resources/unios.png" "$pkgdir/usr/share/pixmaps/unidesk.png"
        install -Dm644 "$startdir/resources/unios.png" "$pkgdir/usr/share/icons/hicolor/128x128/apps/unidesk.png" 
        ICON="unidesk"
    else
        echo "==> ERROR: resources/unios.png not found in $startdir"
        ICON="system-help"
    fi

    cat << EOF > "$pkgdir/usr/share/applications/unidesk.desktop"
[Desktop Entry]
Type=Application
Name=UniDesk
GenericName=UniOS Welcome App
Exec=unidesk
Icon=$ICON
Terminal=false
StartupNotify=true
StartupWMClass=UniDesk
Categories=Utility;System;Qt;
EOF

    cp "$pkgdir/usr/share/applications/unidesk.desktop" "$pkgdir/etc/xdg/autostart/"
}