cmake_minimum_required(VERSION 3.0.2)
project(robot_simulation)


find_package(catkin REQUIRED COMPONENTS
  gazebo_plugins
  gazebo_ros
  gazebo_ros_control
  geometry_msgs
  message_generation
  nav_msgs
  rosbag
  roscpp
  rospy
  sensor_msgs
  std_msgs
  std_srvs
  tf
  tf2
  tf2_geometry_msgs
  tf2_ros
  urdf
  visualization_msgs
  xacro
)
include_directories(include ${catkin_INCLUDE_DIRS})

## Find gazebo
find_package(gazebo REQUIRED)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GAZEBO_CXX_FLAGS}")
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})
find_package(PCL REQUIRED)
## Find Boost
find_package(Boost REQUIRED COMPONENTS thread)
include_directories(${Boost_INCLUDE_DIRS})
include_directories(${PCL_INCLUDE_DIRS})
catkin_package(
 INCLUDE_DIRS include
 LIBRARIES
 CATKIN_DEPENDS rosbag roscpp rospy sensor_msgs std_msgs urdf xacro geometry_msgs nav_msgs tf message_runtime visualization_msgs
)

add_library(nexus_ros_force_based_move src/nexus_ros_force_based_move.cpp)
target_link_libraries(nexus_ros_force_based_move ${Boost_LIBRARIES} ${GAZEBO_LIBRARIES} ${catkin_LIBRARIES})

include_directories(
  ${catkin_INCLUDE_DIRS}
)

# velodyen仿真

link_directories(
  ${GAZEBO_LIBRARY_DIRS}
)




install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
