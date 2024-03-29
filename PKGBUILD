# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Guillaume ALAUX <guillaume@archlinux.org>
# Contributor: Kristof JOZSA <kristof.jozsa@gmail.com>

pkgname=visualvm
pkgver=2.1.3
_shortver=${pkgver//\./}
pkgrel=1
pkgdesc='Visual tool integrating several commandline JDK tools and lightweight profiling capabilities'
url='https://visualvm.github.io/'
arch=('x86_64')
license=('custom:GPL')
depends=('java-environment')
source=(https://github.com/visualvm/visualvm.src/releases/download/${pkgver}/${pkgname}_${_shortver}.zip
        visualvm.desktop
        icon.png)
sha256sums=('3f3388bf61718defdde12d000e2ffd744399eb35fe58f9ee9fc2496901f5e73e'
            'e820807e8d78446cf156a3947d97856e24865bb0d8c957e9ce2fed309c737441'
            '452fbd85c968ec7176c5894bc4106b7e25310314d44278d807510675b6a5c864')

package() {
  cd ${pkgname}_${_shortver}

  install -d "${pkgdir}/usr/share/${pkgname}"
  cp -R bin platform visualvm "${pkgdir}/usr/share/${pkgname}"

  install -d "${pkgdir}/etc/${pkgname}"
  cp -R etc/* "${pkgdir}/etc/${pkgname}"
  ln -s /etc/${pkgname} "${pkgdir}/usr/share/${pkgname}/etc"
    # 'visualvm' shell script cannot even set his own variable 'visualvm_jdkhome'
  sed -i \
    -e 's|#visualvm_jdkhome="/path/to/jdk"|visualvm_jdkhome="${JAVA_HOME}"|' \
    -e 's|visualvm_default_options="|visualvm_default_options="-J-Dawt.useSystemAAFontSettings=on |' \
      "${pkgdir}/etc/${pkgname}/visualvm.conf"

  rm -rf "${pkgdir}"/usr/share/${pkgname}/profiler/lib/deployed/jdk*/{hpux*,mac,solaris*,windows*,linux-arm*}
  if [ ${CARCH} == 'i686' ]; then
    rm -rf "${pkgdir}"/usr/share/${pkgname}/profiler/lib/deployed/jdk*/linux-amd64 \
           "${pkgdir}"/usr/share/${pkgname}/platform/modules/lib/amd64
  else
    rm -rf "${pkgdir}"/usr/share/${pkgname}/profiler/lib/deployed/jdk*/linux \
           "${pkgdir}"/usr/share/${pkgname}/platform/modules/lib/i386
  fi

  find "${pkgdir}"/usr/share/${pkgname} \( -name "*.exe" -o -name "*.dll" \) -delete

  install -d "${pkgdir}/usr/bin"
  ln -s /usr/share/${pkgname}/bin/visualvm "${pkgdir}/usr/bin/${pkgname}"

  install -Dm 644 "${srcdir}/icon.png" -t "${pkgdir}/usr/share/${pkgname}"
  install -Dm 644 "${srcdir}/visualvm.desktop" -t "${pkgdir}/usr/share/applications"

  install -Dm 644 LICENSE.txt -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
