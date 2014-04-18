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
source=("http://xiangzhai.github.io/$pkgname/releases/$pkgname-$pkgver-$pkgrel.src.rpm")
md5sums=('14ad604ad0db726a69a23ba69f95a8e8') #generate with 'makepkg -g'

prepare() {
    cd "$srcdir"

    tar xvf android-utils-4.4-r1.tar.gz
    
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
