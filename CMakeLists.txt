cmake_minimum_required(VERSION 2.8.3)
project(kuka_lwr4_description)

find_package(catkin REQUIRED COMPONENTS xacro)

catkin_package(CATKIN_DEPENDS xacro)

# generate and install URDFs from xacro files
# source: http://wiki.ros.org/xacro#Building_from_CMakeLists.txt

# find all LWR robots with tools
file(GLOB xacro_files ${CMAKE_CURRENT_SOURCE_DIR}/robots/lwr_*.urdf.xacro)

foreach(it ${xacro_files})
  # remove .xacro extension
  string(REGEX MATCH "(.*)[.]xacro$" unused ${it})
  set(output_filename ${CMAKE_MATCH_1})

  # create a rule to generate ${output_filename} from {it}
  xacro_add_xacro_file(${it} ${output_filename})

  list(APPEND urdf_files ${output_filename})
endforeach(it)

add_custom_target(media_files ALL DEPENDS ${urdf_files})


foreach(dir calibration defs meshes robots)
   install(DIRECTORY ${dir}/
      DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
