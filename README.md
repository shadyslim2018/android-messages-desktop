# Android Messages Desktop

**Android Messages Desktop** is a lightweight Electron wrapper for [Google Messages for Web](https://messages.google.com/web/), letting you read and send SMS/RCS messages from a native‑feeling Linux application with desktop notifications, tray integration, and launcher entry.

---

## ✨ Features

- Stand‑alone window for Google Messages  
- System‑tray icon with context menu  
- Minimise‑to‑tray & single‑instance lock  
- Native desktop notifications  
- External links open in your default browser  
- Launcher entry & icon installed system‑wide  

---

## 🧰 Requirements

| Component | Purpose | Version |
|-----------|---------|---------|
| **Node.js** | build/runtime tooling | ≥ 18 |
| **npm**    | dependency manager    | comes with Node |
| **git**    | source retrieval      | any |
| **base‑devel** (Arch/Manjaro) | needed for `makepkg` | latest |

---

## 🚀 Installation

### 1. Local (any Linux distribution)

```bash
git clone https://github.com/shadyslim2018/android-messages-desktop.git
cd android-messages-desktop
npm install          # fetch dependencies
npm start            # run in development mode
```

**Build a distributable (AppImage, deb, rpm, etc.)**

```bash
npm run dist         # output goes to dist/
```

---

### 2. Native Arch / Manjaro package (PKGBUILD)

A ready‑to‑use **PKGBUILD** is included for a proper system package.

```bash
git clone https://github.com/shadyslim2018/android-messages-desktop.git
cd android-messages-desktop
makepkg -si          # build & install (will ask for sudo)
```

- Installs to `/opt/android-messages-desktop/`
- Adds a launcher entry and icon

To uninstall later:

```bash
sudo pacman -Rns android-messages-desktop
```

---

## 📦 Included PKGBUILD (full script)

```bash
# Maintainer: AK
pkgname=android-messages-desktop
pkgver=1.0.0
pkgrel=1
pkgdesc="Electron wrapper for Google Messages (Android Messages) Web"
arch=('x86_64')
url="https://github.com/shadyslim2018/android-messages-desktop"
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
```

---

## 🛠 Troubleshooting

| Problem | Fix |
|---------|-----|
| **Blank/white window** | Check your internet connection and ensure `messages.google.com` isn’t blocked. |
| **App won’t start** | Verify Node ≥ 18 (`node -v`) and confirm `npm install` finished without errors. |

---

## 🤝 Contributing

Pull requests and issues are welcome!  
Please keep PRs focused and follow conventional commit messages.

---

## 📄 License

This project is released under the [MIT License](LICENSE).

> Google Messages is a trademark of Google LLC.  
> This project is independent and not endorsed by Google.
