# Maintainer: Leslie Zhai <xiang.zhai@i-soft.com.cn>

pkgname=apkutil
pkgver=4.4
pkgrel=5
pkgdesc="Apk Utility"
arch=('x86_64')
url="http://xiangzhai.github.io/$pkgname/"
license=('GPL')
depends=('libpng')
makedepends=('rpmextract')
options=('emptydirs')
source=(http://xiangzhai.github.io/$pkgname/releases/$pkgname-$pkgver-$pkgrel.src.rpm
        http://iweb.dl.sourceforge.net/project/libpng/libpng16/older-releases/1.6.7/libpng-1.6.7.tar.xz
        android-utils-4.4-r1-aapt-Makefile.patch
        android-utils-4.4-r1-aapt-Images.patch
       )
       
# generate with 'makepkg -g'
md5sums=('14ad604ad0db726a69a23ba69f95a8e8'
         '7023a9eacd7b6a3eb95761a2f574d456'
         'db9551ff851b967efe96bc9174f5f3e2'
         '40b26c9577d93b769f4452a4359ea75d')

prepare() {
    cd "$srcdir"

    tar xvf android-utils-4.4-r1.tar.gz
    patch -Np0 -i "$srcdir/android-utils-4.4-r1-aapt-Makefile.patch"
    patch -Np0 -i "$srcdir/android-utils-4.4-r1-aapt-Images.patch"

    tar xvf dalvikvm.tar.gz
}

build() {
    cd "$srcdir/android-utils-4.4-r1"
    ./autogen.sh
    ./configure --prefix=/usr
    make

    cd "$srcdir/dalvikvm"
    make
}

package() {                                                                        
    cd "$srcdir/android-utils-4.4-r1"
    make DESTDIR=="${pkgdir}" install
}
