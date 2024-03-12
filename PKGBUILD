# Maintainer: Noah Vogt (noahvogt) noah@noahvogt.com
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=wget-xdg
pkgver=1.24.5
pkgrel=1
pkgdesc='Network utility to retrieve files from the Web - but moving ~/.wget-hsts to $XDG_CACHE_HOME/wget/hsts'
url='https://www.gnu.org/software/wget/wget.html'
arch=('x86_64')
license=('GPL3')
depends=('glibc' 'zlib' 'gnutls' 'libidn2' 'libidn2.so' 'util-linux-libs' 'libuuid.so'
         'libpsl' 'libpsl.so' 'pcre2' 'nettle' 'libnettle.so')
optdepends=('ca-certificates: HTTPS downloads')
backup=('etc/wgetrc')
source=(https://ftp.gnu.org/gnu/${pkgname%-*}/${pkgname%-*}-${pkgver}.tar.lz{,.sig}
        xdg-compliant-wget-hsts-file.patch)
sha256sums=('57a107151e4ef94fdf94affecfac598963f372f13293ed9c74032105390b36ee'
            'SKIP'
            'e7f03d1f253e4b66c38271f4a47ae8d849ac6241c60728b56be1a10b94611293')
b2sums=(
'8057e5992ddaf39b3daffbde99871ddec1328c6bbafbc6b9f1d3cd294bb928b2a80f813024d4cd664c396f84477f1d93d5a21c60c6fe2932f9196d29bb9aa896'
'SKIP'
'0da265b080a193805605bb8705e69e43a07aef062205ae9cf3558ac5e1199b67275f406337153018af4ec1631ef066cdd6eebbd5ba8029b3855e8c71c5953b2e')
validpgpkeys=(
  'AC404C1C0BF735C63FF4D562263D6DF2E163E1EA' # Giuseppe Scrivano <gscrivano@gnu.org>
  '7845120B07CBD8D6ECE5FF2B2A1743EDA91A35B6' # Darshit Shah <darnir@gnu.org>
  '1CB27DBC98614B2D5841646D08302DB6A2670428' # Tim Rühsen <tim.ruehsen@gmx.de>
)
provides=('wget')
conflicts=('wget')

prepare() {
  cd ${pkgname%-*}-${pkgver}
  patch -p1 -i ../xdg-compliant-wget-hsts-file.patch
  cat >> doc/sample.wgetrc <<EOF
# default root certs location
ca_certificate=/etc/ssl/certs/ca-certificates.crt
EOF
}

build() {
  cd ${pkgname%-*}-${pkgver}
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --disable-rpath \
    --enable-nls \
    --with-ssl=gnutls
  make
}

package() {
  cd ${pkgname%-*}-${pkgver}
  make DESTDIR="${pkgdir}" install
}

# vim: ts=2 sw=2 et:
