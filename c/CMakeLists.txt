# This file is part of the OpenKinect Project. http://www.openkinect.org
#
# Copyright (c) 2010 individual OpenKinect contributors. See the CONTRIB file
# for details.
#
# This code is licensed to you under the terms of the Apache License, version
# 2.0, or, at your option, the terms of the GNU General Public License,
# version 2.0. See the APACHE20 and GPL2 files for the text of the licenses,
# or the following URLs:
# http://www.apache.org/licenses/LICENSE-2.0
# http://www.gnu.org/licenses/gpl-2.0.txt
#
# If you redistribute this file in source form, modified or unmodified, you
# may:
#   1) Leave this header intact and distribute it under the same terms,
#      accompanying it with the APACHE20 and GPL20 files, or
#   2) Delete the Apache 2.0 clause and accompany it with the GPL2 file, or
#   3) Delete the GPL v2 clause and accompany it with the APACHE20 file
# In all cases you must keep the copyright notice intact and include a copy
# of the CONTRIB file.
#
# Binary distributions must follow the binary distribution requirements of
# either License.

PROJECT(libfreenect)
set (PROJECT_VER_MAJOR 0)
set (PROJECT_VER_MINOR 0)
set (PROJECT_VER_PATCH 0)
set (PROJECT_VER 
	"${PROJECT_VER_MAJOR}.${PROJECT_VER_MINOR}.${PROJECT_VER_PATCH}")
set (PROJECT_APIVER 
	"${PROJECT_VER_MAJOR}.${PROJECT_VER_MINOR}")

cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/Modules/")

set(CMAKE_C_FLAGS "-Wall -O3 -g")

# Find the host operating system and architecture
include (FindOS)
# Set up installation directories
include (SetupDirectories)

# Add source directories
add_subdirectory (lib)
add_subdirectory (examples)

# Create an uninstall target
configure_file(
    "${CMAKE_SOURCE_DIR}/Modules/UninstallTarget.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/UninstallTarget.cmake"
    IMMEDIATE @ONLY)

add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/UninstallTarget.cmake)
