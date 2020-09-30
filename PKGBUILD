# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname=geoclue_fake-local
pkgver=r6.0d7f9aa
pkgrel=1
pkgdesc="Geoclue Service Faker (installed from local repository)"
arch=('i686' 'x86_64')
url=""
license=('GPL3')
groups=()
depends=('dbus')
#makedepends=('cargo' 'git')
makedepends=('git')
provides=("geoclue2=2.5.2-3" "geoclue=2.5.2-3")
conflicts=("geoclue")
replaces=('geoclue')
backup=('etc/geoclue_fake.toml')
options=()
install=
source=("$pkgname::git+https://github.com/Grollicus/geoclue_fake.git")
noextract=()
md5sums=('SKIP')

pkgver() {
    cd "$pkgname"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$pkgname"
	cargo build --release
}

clean() {
    cd "$pkgname"
	cargo clean
}

package() {
	cd "$pkgname"
    install -Dm755 "target/release/geoclue_fake" "$pkgdir/usr/bin/geoclue_fake"

    install -Dm644 "geoclue_fake.service" "$pkgdir/usr/lib/systemd/system/geoclue_fake.service"
    install -Dm644 "org.freedesktop.GeoClue2.service" "$pkgdir/usr/share/dbus-1/system-services/org.freedesktop.GeoClue2.service"
    install -Dm644 "org.freedesktop.GeoClue2.conf" "$pkgdir/usr/share/dbus-1/system.d/org.freedesktop.GeoClue2.conf"
    install -Dm644 "config.default.toml" "$pkgdir/etc/geoclue_fake.toml"
}
