# Maintainer: Prince Paul <prince dot paul dot k at gmail dot com>

pkgname=python-pyrotgfork
provides=("${pkgname%-git}" python-pyrogram)
conflicts=("${pkgname%-git}" python-pyrogram)
replaces=(python-pyrogram) # pyrogram is dead
pkgver=2.2.12.r4874.c253e6e
pkgrel=1
pkgdesc="A fork of Pyrogram, an elegant, modern and asynchronous Telegram MTProto API framework in Python for users and bots"
arch=("any")
url="https://github.com/TelegramPlayground/pyrogram"
license=("LGPL-3.0-or-later")
depends=("python" "python-aiosqlite" "python-pyaes" "python-pysocks" "python-pymediainfo")
optdepends=(
  "python-tgcrypto: faster cryptography"
  "python-uvloop: fast, drop-in replacement of the built-in asyncio event loop"
)
makedepends=("git" "python-build" "python-installer" "python-wheel" "python-hatchling" "python-setuptools")
checkdepends=("python-pytest" "python-pytest-asyncio" "python-pytest-cov")
source=("${pkgname}::git+${url}.git"
        "fix-test-stringify.patch")

sha256sums=('SKIP'
            '822914b83321a205a14e5a7960e0246bf71785644ea918d88f628070bc349a67')

pkgver() {
  cd "${pkgname}"
  printf "%s.r%s.%s" "$(grep __version__ pyrogram/__init__.py | cut -d '"' -f 2)" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

prepare() {
  cd "${pkgname}"
  patch -p1 < ../fix-test-stringify.patch
}

build() {
  cd "${pkgname}"
  python -m build --wheel --no-isolation
}

check() {
  cd "${pkgname}"
  pytest
}

package() {
  cd "${pkgname}"
  python -m installer --destdir="$pkgdir" dist/*.whl
  echo "Removing wheel packages..."
  rm -rf dist/*.whl
}
