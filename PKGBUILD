# Maintainer:  Caleb Maclennan <caleb@alerque.com>
# Contributor: Adrián Pérez de Castro <aperez@igalia.com>

pkgname=sile-git
pkgdesc='Modern typesetting system inspired by TeX (HEAD version, bundles luarocks)'
pkgver=0.9.5.1.r532.g791c054
pkgrel=1
arch=(any)
url='https://www.sile-typesetter.org'
license=('MIT')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
depends=('fontconfig'
         'harfbuzz>=1.4.2'
         'lua'
         'icu'
         'ttf-gentium-plus')
optdepends=('luajit')
makedepends=('git'
             'luarocks')
checkdepends=('lua-busted'
              'lua-luacov=0.8')
source=("git://github.com/sile-typesetter/${pkgname%-git}.git"
        "git://github.com/sile-typesetter/libtexpdf.git")
sha512sums=('SKIP' 'SKIP')

pkgver() {
    cd "${pkgname%-git}"
    git describe --tags --abbrev=7 --match="v*" HEAD | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare () {
    cd "${pkgname%-git}"
    git submodule init
    git config submodule.libtexpdf.url "$srcdir/libtexpdf"
    git submodule update
    ./bootstrap.sh
}

build () {
    cd "${pkgname%-git}"
    ./configure --prefix=/usr --without-system-luarocks
    make all
    make docs
    make examples
}

check () {
    cd "${pkgname%-git}"
    make busted
}

package () {
    cd "${pkgname%-git}"
    make install DESTDIR="$pkgdir/"

	for file in README.md documentation/sile.pdf ; do
		install -Dm644 "$file" "$pkgdir/usr/share/doc/$pkgname/$(basename $file)"
	done

	cp -ar examples "$pkgdir/usr/share/doc/$pkgname"

	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
