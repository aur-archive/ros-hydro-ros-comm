# Script generated with import_catkin_packages.py
# For more information: https://github.com/bchretien/arch-ros-stacks
pkgdesc="ROS - ROS communications-related packages, including core client libraries (roscpp, rospy) and graph introspection tools (rostopic, rosnode, rosservice, rosparam)."
url='http://www.ros.org/wiki/ros_comm'

pkgname='ros-hydro-ros-comm'
pkgver='1.10.11'
_pkgver_patch=0
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-catkin)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-hydro-xmlrpcpp
  ros-hydro-rosconsole
  ros-hydro-rostopic
  ros-hydro-rosgraph-msgs
  ros-hydro-roswtf
  ros-hydro-rosmsg
  ros-hydro-rosparam
  ros-hydro-roslaunch
  ros-hydro-rosnode
  ros-hydro-topic-tools
  ros-hydro-rosbag
  ros-hydro-roscpp
  ros-hydro-std-srvs
  ros-hydro-message-filters
  ros-hydro-rospy
  ros-hydro-rosservice
  ros-hydro-ros
  ros-hydro-rosgraph
  ros-hydro-rosout
  ros-hydro-rosmaster
  ros-hydro-rostest)

# roslisp cannot be installed on ARM
if test "$CARCH" == x86_64 || test "$CARCH" == i686 ; then
  ros_depends+=('ros-hydro-roslisp')
fi

depends=(${ros_depends[@]})

_tag=release/hydro/ros_comm/${pkgver}-${_pkgver_patch}
_dir=ros_comm
source=("${_dir}"::"git+https://github.com/ros-gbp/ros_comm-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh -v 2 ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
