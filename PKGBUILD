# Maintainer: graysky <graysky AT archlinux DOT us>

pkgname=nct677x-ck
_pkgname=nct6775
pkgver=1.1
pkgrel=1
pkgdesc="Nuvoton lm-sensor module for Z77-based motherboards.  Supports NCT6775F, NCT6776F, and NCT6779D."
arch=('i686' 'x86_64')
url="https://github.com/groeck/nct6775"
license=('GPLv2')
depends=('linux-ck>=3.9' 'linux-ck<3.10')
makedepends=('linux-ck-headers')
conflicts=('nct677x-ck-git')
install=nct677x.install

# until upstream tags a fresh version that builds against 3.9, this works
source=("https://github.com/groeck/$_pkgname/archive/$_pkgname-v$pkgver.tar.gz")
sha256sums=('420a9ea2eac5028ceeec0e52545ffd66c5e0c8d8712e6bf10a97ffd7f95629f7')

_extramodules=extramodules-3.9-ck
_kernver="$(cat /usr/lib/modules/${_extramodules}/version)"

prepare() {
	# headers location and remove shell dependency on running kernel to figure kern ver
	sed -i -e '/^KERNEL_BUILD/ s,headers-,,' -i -e "s/\$(shell uname -r)/$_kernver/" "$_pkgname-$_pkgname-v$pkgver"/Makefile
}

build() {
	cd "$_pkgname-$_pkgname-v$pkgver"
	make
}

package() {
	cd "$_pkgname-$_pkgname-v$pkgver"
	gzip -9 nct6775.ko
	install -Dm644 nct6775.ko.gz "$pkgdir"/usr/lib/modules/$_kernver/kernel/drivers/hwmon/nct6775.ko.gz
}
