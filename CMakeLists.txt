cmake_minimum_required(VERSION 2.8.3)
project(kuka_lwr4_description)

find_package(catkin REQUIRED COMPONENTS xacro)

catkin_package(CATKIN_DEPENDS xacro)

# generate and install URDFs from xacro files
# source: http://wiki.ros.org/xacro#Building_from_CMakeLists.txt

set(xacro_files
    ${CMAKE_CURRENT_SOURCE_DIR}/robots/lwr_ft.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/robots/lwr_pen.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/robots/lwr_sdh.urdf.xacro
)

xacro_add_files(${xacro_files} INORDER REMAP collision_simple:=0 TARGET media_files INSTALL DESTINATION robots)

foreach(dir meshes)
    install(DIRECTORY ${dir}/
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
