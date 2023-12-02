cmake_minimum_required(VERSION 3.5.0)
project(mujoco_mocap_synchronizer_plugin LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake")
include(ProjectOption)

find_package(catkin REQUIRED COMPONENTS)

find_package(mujoco 2.3.6 REQUIRED)

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a exec_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

###################################
## catkin specific configuration ##
###################################

catkin_package(
  LIBRARIES mujoco_mocap_synchronizer_plugin
  DEPENDS mujoco
)

######################################
## mujoco_mocap_synchronizer_plugin ##
######################################

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_library(mujoco_mocap_synchronizer_plugin
  src/mocap_synchronizer_callback.c
)
target_include_directories(mujoco_mocap_synchronizer_plugin SYSTEM PUBLIC
  ${mujoco_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)
target_link_libraries(mujoco_mocap_synchronizer_plugin
  ${mujoco_LIBRARIES}
  ${catkin_LIBRARIES}
)
install(TARGETS mujoco_mocap_synchronizer_plugin
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_pitasc_mujoco_sim.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
