pkgname=fprintd-custom-prompt
pkgver=2.0.0
pkgrel=1
pkgdesc='CLI to set a custom pam_fprintd authentication prompt'
arch=('any')
url='https://github.com/Walentalien/fprintd-en-us-prompt-override'
license=('CC0-1.0')
depends=('fprintd' 'gettext' 'python')
makedepends=()
provides=('fprintd-en-us-prompt-override')
conflicts=('fprintd-en-us-prompt-override')
replaces=('fprintd-en-us-prompt-override')
install=fprintd-custom-prompt.install
source=('fprintd_prompt.py')
sha256sums=('7ff7ad2d9f26459c8c0dd271f55777e071e4641da4419e3d7fb70fa735b1cbda')

package() {
    install -Dm755 "$srcdir/fprintd_prompt.py" \
        "$pkgdir/usr/bin/fprintd-prompt"

    install -d "$pkgdir/usr/share/locale/en_US/LC_MESSAGES"
    ln -s /var/lib/fprintd-custom-prompt/fprintd.mo \
        "$pkgdir/usr/share/locale/en_US/LC_MESSAGES/fprintd.mo"

    install -d "$pkgdir/var/lib/fprintd-custom-prompt"
}
