cmake_minimum_required(VERSION 2.8.3)
project(mono-slam)
set(CMAKE_CXX_FLAGS "-O2 -msse4 -DEIGEN_NO_DEBUG -DNDEBUG")

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
		cv_bridge
		geometry_msgs
		image_geometry
		image_transport
		roscpp
		rospy
		sensor_msgs
		std_msgs
		std_srvs
		tf
		)
find_package(Boost REQUIRED COMPONENTS system)

catkin_package(
		INCLUDE_DIRS include
		CATKIN_DEPENDS cv_bridge geometry_msgs image_geometry image_transport roscpp rospy sensor_msgs std_msgs std_srvs tf
)

include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_executable(${PROJECT_NAME}
		src/monoslam_ransac.cpp 
		#src/camOCV.cpp 
		src/vslamRansac.cpp 
		src/RosVSLAMRansac.cpp 
		src/Patch.cpp 
		src/utils.cpp
		src/libblur.cpp
		src/ConfigVSLAM.cpp
	 	src/camModel.cpp
		)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} config++)
add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

