# Contributor: Piotr Gorski <prgorski88@gmail.com>
# Maintainer: Piotr Gorski <prgorski88@gmail.com>

pkgname=skype2
pkgver=2.2.0.35
pkgrel=6
arch=(i686 x86_64)
pkgdesc="P2P software for high-quality voice communication"
url="http://www.skype.com/"
license=('custom')
options=('!strip')
install=skype.install
depends=(xdg-utils hicolor-icon-theme)
conflicts=('skype-staticqt' 'skype')

if [[ $CARCH == i686 ]]; then
  depends+=(qt4 alsa-lib libxss libxv libxcursor)
  optdepends=('v4l-utils: webcam support'
              'libcanberra: XDG sound support'
              'pulseaudio: PulseAudio support')
else
  depends+=(lib32-{qt4,alsa-lib,libxss,libxv,libxcursor})
  optdepends=('lib32-v4l-utils: webcam support'
              'lib32-libcanberra: XDG sound support'
              'lib32-libpulse: PulseAudio support')
  conflicts+=(bin32-skype bin32-skype-staticqt)
  provides=("bin32-skype=$pkgver")
  replaces=(bin32-skype)
fi

source=(http://download.skype.com/linux/skype-$pkgver.tar.bz2 PERMISSION)
md5sums=('b60a19345ee7b3522b5fe4047150aaf8'
         '26e1772379d4d4df9471b6ed660a6d97')

package() {
  cd "$srcdir/skype-$pkgver"

  # Executable
  install -D skype "$pkgdir/usr/bin/skype"

  # Data
  mkdir -p "$pkgdir"/usr/share/skype/{avatars,lang,sounds}
  install -m 644 avatars/* "$pkgdir/usr/share/skype/avatars"
  install -m 644 lang/*    "$pkgdir/usr/share/skype/lang"
  install -m 644 sounds/*  "$pkgdir/usr/share/skype/sounds"

  # DBus Service
  install -Dm 644 skype.conf \
    "$pkgdir/etc/dbus-1/system.d/skype.conf"

  # Icons
  for _i in 16 32 48; do
    install -Dm 644 icons/SkypeBlue_${_i}x${_i}.png \
      "$pkgdir/usr/share/icons/hicolor/${_i}x${_i}/skype.png"
  done
  install -Dm 644 icons/SkypeBlue_48x48.png \
    "$pkgdir/usr/share/pixmaps/skype.png"

  # Desktop file
  install -Dm 644 skype.desktop \
    "$pkgdir/usr/share/applications/skype.desktop"

  # License
  install -Dm 644 LICENSE \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm 644 "$srcdir/PERMISSION" \
    "$pkgdir/usr/share/licenses/$pkgname/PERMISSION"
}

