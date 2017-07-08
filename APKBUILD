# Contributor: INOUE Yosuke <inoue@kamikakushi.net>
# Maintainer: INOUE Yosuke <inoue@kamikakushi.net>
_pkgrev=0

_kernlevel=$(uname -r)
_kernver=$(printf '%s' "${_kernlevel}" | cut -d'-' -f1)
_kernrev=$(printf '%s' "${_kernlevel}" | cut -d'-' -f2)
_flavor=$(printf '%s' "${_kernlevel}" | cut -d'-' -f3)
_kernpkgver="${_kernver}-r${_kernrev}"

pkgname=pt3-drv-${_flavor}
pkgver=${_kernver}
pkgrel=$((${_kernrev} + ${_pkgrev}))
pkgdesc="PT3 chardev driver"
url="https://github.com/m-tsudo/pt3"
arch="x86 x86_64"
license="GPL3"

_branch="master"
source="https://github.com/m-tsudo/pt3/archive/${_branch}.zip"
builddir="${srcdir}/pt3-${_branch}"

install_if="linux-${_flavor}=${_kernpkgver}"
depends=""
makedepends="linux-${_flavor}-dev=${_kernpkgver}"

build() {
	cd "${builddir}"
	make KVER="${_kernlevel}" || return 1
}

package() {
	cd "${builddir}"

	(
	_instdir="${pkgdir}/lib/modules/${_kernlevel}/kernel/drivers/video"
	_target="${builddir}/pt3_drv.ko"

	# this procedure is as same as Makefile's one but not invoke `depmod`
	install -d "${_instdir}" || return 1
	install -m 644 "${_target}" "${_instdir}" || return 1
	)
}

md5sums="625527eabba2a0b02eca3c8a6f3c4e96  master.zip"
sha256sums="111b26a2c18c52cf9fe4ce5b36de0027d9c950758f0c4874363120c87da6b187  master.zip"
sha512sums="2af6f11755927dccb99cb82e334a2554ddeffe3d5e2e92dd244be64478aa9c71c74d586378609fe3e51715f6489c3cc95fff86a5e4def6ba6c04598e4d5abbaa  master.zip"

