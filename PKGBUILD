# Maintainer: Jesse Spangenberger <azulephoenix@gmail.com>
# Contributor: Tristelune <tristelune@archlinux.info>
pkgname=pdfstudio
pkgver=10.3.0
_pkgver=v10_3_0
pkgrel=1
pkgdesc="Review, annotate, and edit PDF Documents"
arch=('i686' 'x86_64')
url="http://www.qoppa.com/pdfstudio/"
license=('custom')
conflicts=('pdfstudio8' 'pdfstudio9')
provides=('pdfstudio')
makedepends=('pacman>=4.2.0')
depends=('java-runtime' 'desktop-file-utils')
depends_x86_64=('gcc-libs-multilib')

install=${pkgname}.install     
     
sha256sums=('576e81cf3f760370f435060d765b1e58044e594eaa2099dd0dcbba5e92c59958'
            'b82acfb50e1e15a43c54aba7a0712b6c710c10ae74280a26a451343720e965e3'
            '0a3c1c337a22228f3df28412ca65d45d0d8067b508cf7b1cf93810fc17c9b447')
sha256sums_i686=('d199f9924a6241267b06ffd6d3f8e941ef26bb9fbbcfc2d8cfc67a730e126688')
sha256sums_x86_64=('4a7f5234e4fdae8cd1ee139dbc0d32aacbf78389a8042c28cb96c55abb4cb409')
source_i686=("http://www.qoppa.com/files/pdfstudio/demo/downloads/version10/PDFStudio_${_pkgver}_linux.deb")
source_x86_64=("http://www.qoppa.com/files/pdfstudio/demo/downloads/version10/PDFStudio_${_pkgver}_linux64.deb")
source=(${pkgname}.desktop
	${pkgname}.install
	${pkgname}.png)

package() {

	cd "${srcdir}"
	
	bsdtar -xf data.tar.gz 
	bsdtar -xf "${srcdir}/opt/pdfstudio10/lib/pdfstudio.jar" resources/license.html
	
	rm -r "${srcdir}/opt/pdfstudio10/jre"
		
	install -dm 755 "${pkgdir}/opt"
	install -Dm644 ${pkgname}.desktop "${pkgdir}/usr/share/applications/${pkgname}.desktop"
	install -Dm644 ${pkgname}.png "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
	install -Dm644 resources/license.html "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.html"
	
	cp -r opt/ "${pkgdir}"
	mkdir -p "${pkgdir}/usr/bin"
	ln -s /opt/pdfstudio10/pdfstudio10 "${pkgdir}/usr/bin/pdfstudio"
}
