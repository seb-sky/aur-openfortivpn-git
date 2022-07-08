# Maintainer: Olliver Schinagl <oliver@schinagl.nl>

pkgname='openfortivpn-git'
pkgdesc="An open implementation of Fortinet's proprietary PPP+SSL VPN solution"
pkgver='1.17.3.20220621'
_commit='8263c26822c977c2ed92f1ed6b8500067704227f'
pkgrel=0
url='https://github.com/adrienverge/openfortivpn'
arch=('x86_64')
license=('GPL3')
makedepends=(
	'git'
)
depends=(
	'glibc'
	'openssl'
	'ppp'
	'resolvconf'
	'systemd-libs'
)
provides=("openfortivpn=${pkgver}")
conflicts=('openfortivpn')
backup=('etc/openfortivpn/config')
source=("${pkgname}.tar.gz::https://github.com/adrienverge/openfortivpn/archive/${_commit}.tar.gz")
sha512sums=('132c644842fe1490cb5983ca7d906c28d634f78b3273be299a8579a3337d7b03318092e9cacb3ffe198edcfae4adcf5e323756589adf5efa216a8157f807fdbc')
builddir="${pkgname%%-git}-${_commit}"

prepare() {
	cd "${srcdir}/${builddir}"
	sed -i "s|^\(AC_INIT(\[openfortivpn\], \[\).*$|\1${pkgver}-g$(echo "${_commit}" | cut -c 1-9)])|" 'configure.ac'
	autoreconf --force --install --verbose
}

build() {
	cd "${srcdir}/${builddir}"
	./configure \
	            --prefix='/usr' \
	            --sysconfdir='/etc' \
	            --enable-resolvconf \
		    ;
	make
}

package() {
	cd "${srcdir}/${builddir}"
	make DESTDIR="${pkgdir}" install
}
