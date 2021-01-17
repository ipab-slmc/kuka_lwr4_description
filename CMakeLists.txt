cmake_minimum_required(VERSION 3.0.2)
project(kuka_lwr4_description)

find_package(catkin REQUIRED COMPONENTS xacro)

catkin_package(CATKIN_DEPENDS xacro)

# generate and install URDFs from xacro files
# source: http://wiki.ros.org/xacro#Building_from_CMakeLists.txt

set(xacro_files
    ${CMAKE_CURRENT_SOURCE_DIR}/urdf/lwr.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/urdf/lwr_ft.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/urdf/lwr_pen.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/urdf/lwr_sdh.urdf.xacro
    ${CMAKE_CURRENT_SOURCE_DIR}/urdf/lwr_robotiq_3finger.urdf.xacro
)

xacro_add_files(${xacro_files} REMAP collision_simple:=0 TARGET media_files INSTALL DESTINATION urdf)

install(DIRECTORY srdf
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

foreach(dir meshes)
    install(DIRECTORY ${dir}/
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
