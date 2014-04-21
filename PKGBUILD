# Maintainer: Leslie Zhai <xiang.zhai@i-soft.com.cn>

pkgname=apkutil
pkgver=4.4
pkgrel=5
pkgdesc="Android apk development/decompile/compile utilities"
arch=('x86_64')
url="http://xiangzhai.github.io/$pkgname/"
license=('GPL')
depends=('java-environment' 'libpng' 'openssl' 'expat' 'unzip')
makedepends=('rpmextract')
options=('emptydirs')
install=$pkgname.install
source=(http://xiangzhai.github.io/$pkgname/releases/$pkgname-$pkgver-$pkgrel.src.rpm
        http://iweb.dl.sourceforge.net/project/libpng/libpng16/older-releases/1.6.7/libpng-1.6.7.tar.xz
        android-utils-4.4-r1-aapt-Makefile.patch
        android-utils-4.4-r1-aapt-Images.patch
        apkutil.patch
       )
       
# generate with 'makepkg -g'
md5sums=('14ad604ad0db726a69a23ba69f95a8e8'
         '7023a9eacd7b6a3eb95761a2f574d456'
         'db9551ff851b967efe96bc9174f5f3e2'
         '2d8f3819cda983e89c930114b37bfef0'
         '0e1cb89ae8766f834cba4ad7b00bdcc1')

prepare() {
    cd "$srcdir"

    tar xvf android-utils-4.4-r1.tar.gz
    patch -Np0 -i "$srcdir/android-utils-4.4-r1-aapt-Makefile.patch"
    patch -Np0 -i "$srcdir/android-utils-4.4-r1-aapt-Images.patch"

    patch -Np0 -i "$srcdir/apkutil.patch"

    tar xvf signapk.tar.gz

    tar xvf dalvikvm.tar.gz

    tar xvf elfhash-0.4.tar.gz
}

build() {
    cd "$srcdir/android-utils-4.4-r1"
    ./autogen.sh
    ./configure --prefix=/usr
    make

    cd "$srcdir/signapk"
    make

    cd "$srcdir/dalvikvm"
    make

    cd "$srcdir/elfhash-0.4"
    make
}

package() {                                                                        
    cd "$srcdir/android-utils-4.4-r1"
    make DESTDIR=$pkgdir install

    cd "$srcdir/elfhash-0.4"
    make DESTDIR=$pkgdir install

    mkdir -p "$pkgdir/usr/share/$pkgname"
    install -m 0755 "$srcdir/$pkgname.sh" "$pkgdir/usr/share/$pkgname"
    ln -sf "$pkgdir/usr/share/$pkgname/$pkgname.sh" "$pkgdir/usr/bin/$pkgname"

    install -m 0755 "$srcdir/template.tar.gz" "$pkgdir/usr/share/$pkgname"

    mkdir -p "$pkgdir/usr/share/$pkgname/signapk"
    install -m 0644 "$srcdir/signapk/signapk.jar" "$pkgdir/usr/share/$pkgname/signapk"
    install -m 0644 "$srcdir/signapk/testkey.pk8" "$pkgdir/usr/share/$pkgname/signapk"
    install -m 0644 "$srcdir/signapk/testkey.x509.pem" "$pkgdir/usr/share/$pkgname/signapk"

    mkdir -p "$pkgdir/usr/share/$pkgname/dalvikvm"
    install -m 0644 "$srcdir/dalvikvm/dalvikvm.jar" "$pkgdir/usr/share/$pkgname/dalvikvm"

    mkdir -p "$pkgdir/usr/share/$pkgname/smali"
    install -m 0644 "$srcdir/smali-2.0b6.jar" "$pkgdir/usr/share/$pkgname/smali/smali.jar"
    install -m 0644 "$srcdir/baksmali-2.0b6.jar" "$pkgdir/usr/share/$pkgname/smali/baksmali.jar"

    mkdir -p "$pkgdir/usr/share/$pkgname/droiddraw"
    tar xvf "$srcdir/droiddraw-r1b22.tgz" -C "$pkgdir/usr/share/$pkgname/droiddraw"
    install -m 0644 "$srcdir/androiddraw-signed.apk" "$pkgdir/usr/share/$pkgname/droiddraw"

    mkdir -p "$pkgdir/usr/share/$pkgname/apktool"
    tar xvf "$srcdir/apktool-install-linux-r05-ibot.tar.bz2" --strip-components=1 -C "$pkgdir/usr/share/$pkgname/apktool"
    tar xvf "$srcdir/apktool1.5.2.tar.bz2" --strip-components=1 -C "$pkgdir/usr/share/$pkgname/apktool"
    
    unzip "$srcdir/dex2jar-0.0.9.15.zip" -d "$pkgdir/usr/share/$pkgname"
    mv "$pkgdir/usr/share/$pkgname/dex2jar-0.0.9.15" "$pkgdir/usr/share/$pkgname/dex2jar"

    tar xvf "$srcdir/android-sdk-4.1.2.tar.gz" -C "$pkgdir/usr/share/$pkgname"

    mkdir -p "$pkgdir/usr/share/$pkgname/soot"
    install -m 0644 "$srcdir/soot-2.5.0.jar" "$pkgdir/usr/share/$pkgname/soot/soot.jar"

    tar xvf "$srcdir/example.tar.gz" -C "$pkgdir/usr/share/$pkgname"
}
