# Maintainer: Your Name <your@email.com>
pkgname=android-messages-desktop
pkgver=1.0.0
pkgrel=1
pkgdesc="Electron wrapper for Google Messages (Android Messages) Web"
arch=('x86_64')
url="https://github.com/yourname/android-messages-desktop"
license=('MIT')
depends=('electron' 'hicolor-icon-theme')
makedepends=('npm' 'nodejs' 'git')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/shadyslim2018/android-messages-desktop/archive/refs/tags/v${pkgver}.tar.gz"
        "icon.png")
sha256sums=('SKIP' 'SKIP')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  npm install
  npx electron-builder --linux --dir
}

package() {
  install -dm755 "${pkgdir}/opt/${pkgname}"
  cp -r "${srcdir}/${pkgname}-${pkgver}/dist/linux-unpacked/"* "${pkgdir}/opt/${pkgname}/"

  # Install desktop launcher
  install -Dm644 /dev/stdin "${pkgdir}/usr/share/applications/${pkgname}.desktop" << EOF
[Desktop Entry]
Type=Application
Name=Android Messages Desktop
Exec=/opt/${pkgname}/android-messages-desktop
Icon=android-messages-desktop
Comment=Electron wrapper for Google Messages (Android Messages) Web
Categories=Network;Chat;
Terminal=false
EOF

  # Install icon
  install -Dm644 "${srcdir}/icon.png" "${pkgdir}/usr/share/icons/hicolor/256x256/apps/android-messages-desktop.png"
}
