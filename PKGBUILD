_pkgname=xfce4-panel
pkgname=${_pkgname}-winxp-tc-git
pkgver=4.16.0+148+gd81b82b8.6402.d81b82b8.92de258b3fdbf9046979488b19147ebd
pkgrel=1
pkgdesc="Panel for the Xfce desktop environment - git version patched for Windows XP Total Conversion"
arch=('x86_64')
url="https://docs.xfce.org/xfce/xfce4-panel/start"
license=('GPL2')
groups=('xfce4-git')
conflicts=("${_pkgname}" 'xfce4-statusnotifier-plugin')
provides=("${_pkgname}=${pkgver%%+*}")
depends=('exo' 'garcon' 'libxfce4ui' 'xfconf' 'libwnck3' 'libdbusmenu-gtk3'
         'hicolor-icon-theme' 'desktop-file-utils')
makedepends=('intltool' 'gobject-introspection' 'vala' 'git' 'xfce4-dev-tools' 'gtk-doc' 
	     'libxfce4ui>=4.17.1' 'libxfce4util>=4.17.1')
optdepends=('xfce4-panel-profiles')
replaces=('xfce4-statusnotifier-plugin')
source=("${_pkgname}::git+https://gitlab.xfce.org/xfce/${_pkgname}"
        'xfce4-panel-winxp-tc.patch')
sha256sums=('SKIP'
            '934829cc2420598fd03e508502a75bc6a5bc8fc488a9c337a0782c20dc8bc185')

pkgver() {
  cd "$srcdir/${_pkgname}"
  local _ver
  _ver="$(git describe --long --tags | sed -r "s:^${_pkgname}.::;s/^v//;s/^xfce-//;s/-/+/g")"
  local _patchver
  local _patchfile
  for _patchfile in "${source[@]}"; do
    _patchfile="${_patchfile%%::*}"
    _patchfile="${_patchfile##*/}"
    [[ $_patchfile = *.patch ]] || continue
    _patchver="${_patchver}$(md5sum ${srcdir}/${_patchfile} | cut -c1-32)"
  done
  _patchver="$(echo -n $_patchver | md5sum | cut -c1-32)"
  echo ${_ver/-/_}.$(git rev-list --count HEAD).$(git rev-parse --short HEAD).${_patchver}
}

prepare() {
  local _patchfile
  for _patchfile in "${source[@]}"; do
    _patchfile="${_patchfile%%::*}"
    _patchfile="${_patchfile##*/}"
    [[ $_patchfile = *.patch ]] || continue
    echo "Applying patch $_patchfile..."
    patch --directory="$srcdir/${_pkgname}" --forward --strip=1 --input="${srcdir}/${_patchfile}"
  done
}

build() {
  cd "$srcdir/${_pkgname}"
  ./autogen.sh \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --disable-static \
    --enable-gio-unix \
    --enable-gtk-doc \
    --disable-debug
  make
}

package() {
  cd "$srcdir/${_pkgname}"
  make DESTDIR="$pkgdir" install
}

