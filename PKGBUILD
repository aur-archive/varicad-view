# Maintainer: gh0st <echo ZGV2QGFudGktc3R1ZGlvLmV1Cg==|base64 -d>
# Contributor: Matjaz Mozetic <rationalperseus at gmail dot com>
# Contributor: Piotr Rogoza <rogoza dot piotr at gmail dot com>

pkgname=varicad-view
_pkgname=varicad2015-view
pkgver=2015.1.09
pkglang=en
_pkglang=en
_pkgver=${pkgver#*.}
pkgrel=1
pkgdesc='Viewer VariCAD files. It can also open STEP (3D), DWG (2D), DXF (2D) and IGES (2D) files.'
arch=('i686' 'x86_64')
url='http://www.varicad.com'
#http://www.varicad.com/userdata/files/release/en
license=('custom')
depends=(hicolor-icon-theme gtk2 desktop-file-utils glu libsm)
install='varicad-view.install'
options=(!strip)

[ "${CARCH}" = "i686" ] && _deb_arch='i386'
[ "${CARCH}" = "x86_64" ] && _deb_arch='amd64'

source=("varicadview.xml"
			"varicadview.patch"
			"http://www.varicad.com/userdata/files/release/${_pkglang}/${_pkgname}-${_pkglang}_${_pkgver}_${_deb_arch}.deb"
		 )
		 	
md5sums+=(
         '0fb9488c57185041c77805a06d9f301e'	#varicadview.xml
         'bbb6573648c21d6a4ff2c2a3b1772f78'	#varicadview.patch
         )	


#CARCH=x86_64
if [ "$CARCH" == i686 ]; then
	_pkgname1=${_pkgname}-${_pkglang}_${_pkgver}_${_deb_arch}.deb
    md5sums+=(
         '0df87db6fcfe4cd57f87cb14af34ef1c')
elif [ "$CARCH" == x86_64 ]; then
	_pkgname1=${_pkgname}-${_pkglang}_${_pkgver}_${_deb_arch}.deb
    md5sums+=(
         'e847cd59de2a79d7a55e9b08311dbd03')
fi		
			
#pkglang sums
#         ''	#de-i386
#         ''	#de-amd64
#         ''	#cz-i386
#         ''	#cz-amd64
#         ''	#pt-i386
#         ''	#pt-amd64



package(){
  cd "$srcdir"
  ar p ${_pkgname1} data.tar.gz | tar zx

  tar -c opt | tar -x -C ${pkgdir}
  tar -c usr | tar -x -C ${pkgdir}
  rm -f $pkgdir/usr/share/doc/varicad2010-view-${_pkglang}/{changelog.gz,copyright,README.Debian}

  cd $srcdir/opt/VariCAD-View/desktop
  install -Dm644 varicadview.desktop \
    $pkgdir/usr/share/applications/varicadview.desktop
  install -Dm644 x-varicadview.desktop \
    $pkgdir/usr/share/mimelnk/application/x-varicadview.desktop
  for i in 16x16 22x22 32x32 48x48; do
    install -Dm 644 varicadview_$i.png \
      $pkgdir/usr/share/icons/hicolor/$i/apps/varicadview.png
  done
  install -Dm 664 varicadview.xpm $pkgdir/usr/share/pixmaps/varicadview.xpm
  install -Dm 664 varicadview.xpm $pkgdir/usr/share/icons/varicadview.xpm

  cd $pkgdir
  ##thx lgomes
  patch -p1 < $srcdir/varicadview.patch
  install -Dm644 $srcdir/varicadview.xml \
    $pkgdir/usr/share/mime/packages/varicadview.xml 
  #
} 
