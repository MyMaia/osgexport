# Copyright (C) 2008 Cedric Pinson
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA.
#
# Authors:
#  Cedric Pinson <cedric.pinson@plopbyte.com>

ADD_CUSTOM_TARGET( copy_blender_testfile ALL
  cmake -E copy_if_different ${PROJECT_SOURCE_DIR}/test/test.blend ${CMAKE_CURRENT_BINARY_DIR}
  )


CONFIGURE_FILE(
  ${CMAKE_CURRENT_SOURCE_DIR}/test-armature.py.in 
  ${CMAKE_CURRENT_BINARY_DIR}/test-armature.py
  IMMEDIATE @ONLY
  )
#animation is not yet implemented on 2.5
#ADD_TEST("test-armature" ${BLENDER} -b ${CMAKE_CURRENT_BINARY_DIR}/test.blend -P test-armature.py --osg="filename=${CMAKE_CURRENT_BINARY_DIR}/${DATA_DEST}\;RELATIVE_PATH=True" )

CONFIGURE_FILE(
  ${CMAKE_CURRENT_SOURCE_DIR}/test-bug_multimaterial.py.in 
  ${CMAKE_CURRENT_BINARY_DIR}/test-bug_multimaterial.py
  IMMEDIATE @ONLY
  )
ADD_TEST("test-bug_multimaterial" ${BLENDER} --background ${CMAKE_CURRENT_BINARY_DIR}/test.blend --python ${CMAKE_CURRENT_BINARY_DIR}/test-bug_multimaterial.py)

CONFIGURE_FILE(
  ${CMAKE_CURRENT_SOURCE_DIR}/test-geometry_and_material.py.in 
  ${CMAKE_CURRENT_BINARY_DIR}/test-geometry_and_material.py
  IMMEDIATE @ONLY
  )
ADD_TEST("test-geometry_and_material" ${BLENDER} --background ${CMAKE_CURRENT_BINARY_DIR}/test.blend --python ${CMAKE_CURRENT_BINARY_DIR}/test-geometry_and_material.py)


CONFIGURE_FILE(
  ${CMAKE_CURRENT_SOURCE_DIR}/test-exporter.py.in 
  ${CMAKE_CURRENT_BINARY_DIR}/test-exporter.py
  IMMEDIATE @ONLY
  )
ADD_TEST("test-exporter" ${BLENDER} --background ${CMAKE_CURRENT_BINARY_DIR}/test.blend --python ${CMAKE_CURRENT_BINARY_DIR}/test-exporter.py)


CONFIGURE_FILE(
  ${CMAKE_CURRENT_SOURCE_DIR}/test-baked_ipo.py.in
  ${CMAKE_CURRENT_BINARY_DIR}/test-baked_ipo.py
  IMMEDIATE @ONLY
  )
#ADD_TEST("test-bake_ipo" ${BLENDER} -b ${CMAKE_CURRENT_BINARY_DIR}/test.blend -P test-baked_ipo.py --osg="filename=${CMAKE_CURRENT_BINARY_DIR}/${DATA_DEST}\;RELATIVE_PATH=True" )


