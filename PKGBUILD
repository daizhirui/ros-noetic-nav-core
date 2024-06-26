# Maintainer: Timon Engelke <aur@timonengelke.de>
pkgdesc="ROS - This package provides common interfaces for navigation specific robot actions."
url='https://wiki.ros.org/nav_core'

pkgname='ros-noetic-nav-core'
pkgver='1.17.3'
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-noetic-std-msgs
  ros-noetic-catkin
  ros-noetic-costmap-2d
  ros-noetic-tf
  ros-noetic-geometry-msgs)
makedepends=('cmake' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-noetic-std-msgs
  ros-noetic-costmap-2d
  ros-noetic-tf
  ros-noetic-geometry-msgs)
depends=(${ros_depends[@]})

# Git version (e.g. for debugging)
# _tag=release/noetic/nav_core/${pkgver}-${_pkgver_patch}
# _dir=${pkgname}
# source=("${_dir}"::"git+https://github.com/ros-gbp/navigation-release.git"#tag=${_tag})
# sha256sums=('SKIP')

# Tarball version (faster download)
_dir="navigation-${pkgver}/nav_core"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-planning/navigation/archive/${pkgver}.tar.gz")
sha256sums=('6500e427f868ea63801203715f41cbec4ed1bd1f9a29ae130a74b3776a7684f6')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
