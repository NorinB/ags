# Modified from AUR package "aylurs-gtk-shell-git" maintained by kotontrion <kotontrion@tutanota.de>
pkgname=norin-ags
_pkgname=ags
pkgver=r551.2376019
pkgrel=1
pkgdesc="Aylurs's Gtk Shell (AGS), version fixed for Norin."
arch=('x86_64')
url="https://github.com/NorinB/ags"
license=('GPL3')
makedepends=('git' 'gobject-introspection' 'meson' 'npm' 'typescript')
depends=('gjs' 'glib2' 'glib2-devel' 'glibc' 'gtk3' 'gtk-layer-shell' 'libpulse' 'pam')
optdepends=('gnome-bluetooth-3.0: required for bluetooth service'
  'greetd: required for greetd service'
  'libdbusmenu-gtk3: required for systemtray service'
  'libsoup3: required for the Utils.fetch feature'
  'libnotify: required for sending notifications'
  'networkmanager: required for network service'
  'power-profiles-daemon: required for powerprofiles service'
  'upower: required for battery service')
conflicts=('aylurs-gtk-shell' 'aylurs-gtk-shell-git')
source=("git+${url}.git#commit=1909b9d332706a8eca193e2f424cc7b48f773dca"
  "git+https://gitlab.gnome.org/GNOME/libgnome-volume-control")
sha256sums=('SKIP'
  'SKIP')

pkgver() {
  cd $srcdir/$_pkgname
  printf 'r%s.%s' "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd $srcdir/$_pkgname
  git submodule init
  git config submodule.subprojects/gvc.url "$srcdir/libgnome-volume-control"
  git -c protocol.file.allow=always submodule update
}

build() {
  cd $srcdir/$_pkgname
  npm install
  arch-meson build --libdir "lib/$_pkgname" -Dbuild_types=true
  meson compile -C build
}

package() {
  cd $srcdir/$_pkgname
  meson install -C build --destdir "$pkgdir"
  ln -sf /usr/share/com.github.NorinB.ags/com.github.NorinB.ags ${pkgdir}/usr/bin/ags
}
