# Maintainer: Limao Luo <luolimao+AUR@gmail.com>
#
# (Added from terminal package)
# Contributor: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: tobias <tobias@archlinux.org>
# Contributor: Aurelien Foret <orelien@chez.com>

_pkgname=terminal
pkgname=$_pkgname-git
pkgver=20121222
pkgrel=1
pkgdesc="A modern terminal emulator primarly for the Xfce desktop environment"
arch=(i686 x86_64)
url=http://www.xfce.org/projects/$_pkgname/
license=(GPL2)
groups=(xfce4-git)
depends=(libxfce4ui-git vte)
makedepends=(git xfce4-dev-tools)
provides=($_pkgname=0.4.8)
conflicts=($_pkgname)
options=(!libtool)
install=$_pkgname.install

_gitroot=git://git.xfce.org/apps/$_pkgname
_gitname=$_pkgname

build() {
    cd "$srcdir"
    msg "Connecting to the GIT server..."
    if [[ -d $_gitname/.git ]]; then
        pushd $_gitname && git pull
        msg2 "The local files are updated."
        popd
    else
        git clone --depth 1 $_gitroot
    fi
    msg2 "GIT checkout done or server timeout"

    rm -rf $_gitname-build/
    cp -r $_gitname/ $_gitname-build/
    cd $_gitname-build/

    msg "Building..."
    ./autogen.sh \
        --prefix=/usr \
        --sysconfdir=/etc \
        --libexecdir=/usr/lib/xfce4 \
        --localstatedir=/var \
        --disable-static \
        --disable-debug
    make
}

package() {
    cd "$srcdir"/$_gitname-build/
    make DESTDIR="$pkgdir" install
}
