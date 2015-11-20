cmake_minimum_required(VERSION 2.8.3)

project(dvo_benchmark)

LIST(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake_modules")

find_package(catkin REQUIRED COMPONENTS roscpp dvo_core dvo_ros dvo_slam)
find_package(cmake_modules REQUIRED)
find_package(Eigen3 REQUIRED)
#find_package(G2O REQUIRED)
find_package(OpenCV 2.4.8 REQUIRED)

#LIST(APPEND CMAKE_CXX_FLAGS "-std=c++11")

set(G2O_LIBS g2o_cli.so
  g2o_core
  g2o_csparse_extension
  g2o_ext_freeglut_minimal
  g2o_incremental
  g2o_interactive
  g2o_interface
  g2o_opengl_helper
  g2o_parser
  g2o_simulator
  g2o_solver_cholmod
  g2o_solver_csparse
  g2o_solver_dense
  g2o_solver_eigen
  g2o_solver_pcg
  g2o_solver_slam2d_linear
  g2o_solver_structure_only
  g2o_stuff
  g2o_types_data
  g2o_types_icp
  g2o_types_sba
  g2o_types_sclam2d
  g2o_types_sim3
  g2o_types_slam2d
  g2o_types_slam3d
)


catkin_package(
  INCLUDE_DIRS include
  LIBRARIES dvo_benchmark
)

include_directories(
  "include"
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
  #${G2O_INCLUDE_DIR}
)

link_directories(
  ${catkin_LIBRARY_DIRS}
)


add_executable(benchmark
     src/benchmark_slam.cpp
)

#add_executable(experiment
#     src/experiment.cpp
#)

target_link_libraries(benchmark
#  vtkCommon
  ${catkin_LIBRARIES}
  ${G2O_LIBS}
)

# create output directory - just convenience for our users
#file(MAKE_DIRECTORY "${PROJECT_SOURCE_DIR}/output")
#file(MAKE_DIRECTORY "${PROJECT_SOURCE_DIR}/output/video")

install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)
