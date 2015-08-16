# Maintainer: Tetsumaki <http://goo.gl/YMBdA>

pkgname=leed-svn
pkgver=99
pkgrel=1
pkgdesc="This project is now on GIT, please use leed-git"
arch=('any')
url="http://projet.idleman.fr/leed/"
license=('CC by-nc-sa')
depends=('php' 'mysql' 'wget')
makedepends=('subversion')
optdepends=('apache: is depedency if you do not use lighttpd or nginx'
            'lighttpd'
            'nginx')
conflicts=('leed-git')
install=${pkgname}.install

_svntrunk=http://projet.idleman.fr/leed.svn/
_svnmod=leed

build() {
	cd "${srcdir}"
	msg "Connecting to SVN server...."

	if [[ -d "${_svnmod}/.svn" ]]; then
		cd "${_svnmod}" && svn up -r ${pkgver}
	else
		svn co ${_svntrunk} --config-dir ./ -r ${pkgver} ${_svnmod}
	fi

	msg "SVN checkout done or server timeout"
	msg "Starting build..."

	rm -rf "${srcdir}/${_svnmod}-build"
	svn export "${srcdir}/${_svnmod}" "${srcdir}/${_svnmod}-build"

	if [ -e "${srcdir}/${_svnmod}-build/logs" ]; then
		cd "${srcdir}/${_svnmod}-build/logs"
		rm -rf *
	fi
}

package() {
	install -dm755 "${pkgdir}/usr/share/webapps/${_svnmod}"
	cd "${srcdir}/${_svnmod}-build"
	cp -rf * "${pkgdir}/usr/share/webapps/${_svnmod}"
	chmod -R 755 "${pkgdir}/usr/share/webapps/${_svnmod}"
}
