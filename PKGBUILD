# Maintainer: Rodrigo Bezerra <rodrigobezerra21 at gmail dot com>
# Contributor: Tod Jackson <tod.jackson@gmail.com>
# Contributor: orumin <dev@orum.in>
# Contributor: Adam <adam900710 at gmail dot com>

_basename=gst-libav
pkgname=lib32-gst-libav
pkgver=1.20.0
pkgrel=1
pkgdesc="Multimedia graph framework - libav plugin (32-bit)"
url="https://gstreamer.freedesktop.org/"
arch=(x86_64)
license=(GPL)
depends=(bzip2 lib32-gst-plugins-base-libs lib32-libffmpeg gst-libav)
makedepends=(python git meson)
provides=("lib32-gst-ffmpeg=$pkgver-$pkgrel")
#_commit=2aa8ef4173294c35bf8c2363f4475976e922e995 # tags/1.19.2^0
source=("https://gstreamer.freedesktop.org/src/gst-libav/gst-libav-1.20.0.tar.xz")
sha256sums=('SKIP')


build() {
    tar -xf "gst-libav-1.20.0.tar.xz" -C .
	echo "working dir"
	pwd

    export CC='gcc -m32'
    export CXX='g++ -m32'
    export PKG_CONFIG='/usr/bin/i686-pc-linux-gnu-pkg-config'

	sed -i "29i gst_plugin_scanner_path = '/usr/lib32/gstreamer-1.0/gst-plugin-scanner'" gst-libav-1.20.0/tests/check/meson.build

	mkdir -p mesonBuild

    arch-meson gst-libav-$pkgver mesonBuild \
        --libdir=lib32 \
        --libexecdir=lib32 \
        -D doc=disabled \
        -D package-name="GStreamer FFmpeg Plugin (Arch Linux)" \
        -D package-origin="https://www.archlinux.org/"


    meson compile -C mesonBuild
}

check() {
    meson test -C mesonBuild --print-errorlogs
}

package() {
    meson install -C mesonBuild --destdir "$pkgdir"
}
