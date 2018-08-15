# zxing-cv/CMakeList.txt
#
# Copyright (C) 2016 Alessandro Francescon
# 
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License.
# 
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 2.8.3)

project(zxing_cv)

find_package(catkin REQUIRED COMPONENTS
	roscpp
        tf
	cv_bridge
	image_transport
	sensor_msgs
        geometry_msgs
        dynamic_reconfigure
	zxing	
	zxing_msgs
)

generate_dynamic_reconfigure_options(cfg/QRDetector.cfg)

include_directories(
	${catkin_INCLUDE_DIRS}
        src
)

add_library(qr_detector_nodelet src/qr_detector_nodelet.cpp src/qr_detector.cpp)

add_dependencies(qr_detector_nodelet qr_detector_gencfg ${catkin_EXPORTED_TARGETS})

target_link_libraries(qr_detector_nodelet
        ${catkin_LIBRARIES}
)

add_executable(qr_detector_node src/qr_detector_node.cpp src/qr_detector.cpp)

add_dependencies(qr_detector_node qr_detector_gencfg ${catkin_EXPORTED_TARGETS})

target_link_libraries(qr_detector_node
        ${catkin_LIBRARIES}
)
