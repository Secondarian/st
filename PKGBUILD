# Maintainer:

pkgname=st
pkgver=0.8.2.r1062.2087ab9
pkgrel=1
epoch=1
pkgdesc="My build of Luke's st with vim-bindings, transparency, xresources, etc."
url='https://github.com/Secondarian/st'
arch=('i686' 'x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
makedepends=('ncurses' 'libxext' 'git')
optdepends=('dmenu: feed urls to dmenu')
source=(git+https://github.com/Secondarian/st)
sha1sums=('SKIP')

provides=("${pkgname}")
conflicts=("${pkgname}")

pkgver() {
	cd "${pkgname}"
	printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
		"$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd $srcdir/${pkgname}
	# skip terminfo which conflicts with ncurses
	sed -i '/tic /d' Makefile
}

build() {
	cd "${pkgname}"
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
	install -Dm644 Xdefaults "${pkgdir}/usr/share/doc/${pkgname}/Xdefaults.example"
}
