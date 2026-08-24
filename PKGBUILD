pkgname=fprintd-en-us-prompt-override
pkgver=1
pkgrel=1
pkgdesc='Custom en_US right-index prompt for pam_fprintd'
arch=('any')
url='https://github.com/Walentalien/fprintd-en-us-prompt-override'
license=('GPL-2.0-or-later')
depends=('fprintd')
makedepends=('gettext')
source=('fprintd.po')
sha256sums=('aef3c7acdba6ea65b923d0af25e2a52e0d15089b688d2e8ab239ff01eeada1ee')
build() {
    msgfmt --check --check-format \
    "$srcdir/fprintd.po" \
    -o "$srcdir/fprintd.mo"
}

package() {
    install -Dm644 "$srcdir/fprintd.mo" \
    "$pkgdir/usr/share/locale/en_US/LC_MESSAGES/fprintd.mo"
}
