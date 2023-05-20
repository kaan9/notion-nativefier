# Maintainer: Alec Mev <alec@mev.earth>
# modified by kaan

pkgname=notion-nativefier
pkgver=2023.05.20
pkgrel=1
pkgdesc='Notion desktop built with nativefier (electron)'
arch=('x86_64')
url='https://www.notion.so'
license=('custom')
license=("custom")
depends=("gtk3" "libxss" "nss")
optdepends=("libindicator-gtk3")
makedepends=("imagemagick" "nodejs-nativefier" "unzip")
source=(
  "${pkgname}.png"
  "${pkgname}.desktop"
)
sha256sums=(
  "6188b8e17b8538643391ba1605d5ebf50f5298f85f74191fdba25ad88d74e0bd"
  "2f77a959abb077cfe4a0ca2d7246e8c519371cde8c891aaa59e0c821a21b8c7a"
)

build() {
  cd "${srcdir}"

  nativefier \
    --name "Notion" \
    --icon "${pkgname}.png" \
    --width "800px" \
    --height "600px" \
    --user-agent "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.3 Chrome/109.0.5414.117 Safari/605.1.15" \
    --verbose \
    --single-instance \
    --tray \
    "${url}"
}

package() {
  install -dm755 "${pkgdir}/"{opt,usr/{bin,share/{applications,licenses/${pkgname}}}}

  _folder=$(ls "${srcdir}" | grep "[Nn]otion-linux-")
  _binary=$(ls "${srcdir}/${_folder}" | grep "[Nn]otion")

  cp -rL "${srcdir}/${_folder}" "${pkgdir}/opt/${pkgname}"
  ln -s "/opt/${pkgname}/${_binary}" "${pkgdir}/usr/bin/${pkgname}"
  install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -Dm644 "${pkgdir}/opt/${pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  for _size in "192x192" "128x128" "96x96" "64x64" "48x48" "32x32" "24x24" "22x22" "20x20" "16x16" "8x8"; do
    install -dm755 "${pkgdir}/usr/share/icons/hicolor/${_size}/apps"
    convert "${srcdir}/${pkgname}.png" -strip -resize "${_size}" "${pkgdir}/usr/share/icons/hicolor/${_size}/apps/${pkgname}.png"
  done
}

#package() {
#  mkdir -p "${pkgdir}/usr/share"
#  local _x=`echo "Notion-linux-"*`
#  cp -r "${_x}/resources/app" "${pkgdir}/usr/share/${pkgname}"
#  install -Dm755 -t "${pkgdir}/usr/bin/" "${pkgname}"
#  install -Dm644 -t "${pkgdir}/usr/share/applications/" "${pkgname}.desktop"
#  install -Dm644 -t "${pkgdir}/usr/share/licenses/${pkgname}" "${_x}/LICENSE"
#  install -Dm644 -t "${pkgdir}/usr/share/pixmaps/" "${pkgname}.png"
#
#  for _size in "192x192" "128x128" "96x96" "64x64" "48x48" "32x32" "24x24" "22x22" "20x20" "16x16" "8x8"; do
#    install -dm755 "${pkgdir}/usr/share/icons/hicolor/${_size}/apps"
#    convert "${srcdir}/${pkgname}.png" -strip -resize "${_size}" "${pkgdir}/usr/share/icons/hicolor/${_size}/apps/${pkgname}.png"
#  done
#}
