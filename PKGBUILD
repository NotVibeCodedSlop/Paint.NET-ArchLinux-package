
pkgname=paintdotnet-wine
pkgver=5.200.9793.3533
pkgrel=3
pkgdesc="Paint.NET running under Wine with DXVK"
arch=('x86_64')
url="https://github.com/paintdotnet/Paint.NET-on-Wine"
license=('LicenseRef-custom')
depends=(
    'wine'
    'winetricks'
    'cabextract'
    'wget'
    'bubblewrap'
    'yad'
)
makedepends=()
options=('!strip')

_archive="paint.net.${pkgver}.portable.x64.wine.EXPERIMENTAL.zip"

source=(
    "${_archive}::https://github.com/paintdotnet/Paint.NET-on-Wine/releases/download/v${pkgver}/${_archive}"
    'paintdotnet'
    'paintdotnet.desktop'
)

# Replace SKIP with the actual SHA-256 after downloading the release.
sha256sums=(
    'SKIP'
    'SKIP'
    'SKIP'
)

package() {
    local appdir="${pkgdir}/opt/paintnetwine"
    local extracted="${srcdir}/paintnetwine"

    install -d "$appdir" "$extracted"

    bsdtar -xf "${srcdir}/${_archive}" -C "$extracted"

    if [[ ! -f "${extracted}/paintdotnet.sh" ]]; then
        error "paintdotnet.sh was not found in the release archive"
        return 1
    fi

    if [[ ! -f "${extracted}/paintdotnet.ico" ]]; then
        error "paintdotnet.ico was not found in the release archive"
        return 1
    fi

    cp -a "${extracted}/." "$appdir/"

    chmod +x "${appdir}/paintdotnet.sh"

    install -Dm755 "${srcdir}/paintdotnet" \
        "${pkgdir}/usr/bin/paintdotnet"

    install -Dm644 "${srcdir}/paintdotnet.desktop" \
        "${pkgdir}/usr/share/applications/paintdotnet.desktop"
}

