﻿# CMakeList.txt : CMake project for PointsCloud, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.5)


project ("PointsCloud")
#允许GDB调试
set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_DEBUG   "$ENV{CXXFLAGS} -o0 -Wall -g -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -o3 -Wall")

#SET(CMAKE_BUILD_TYPE Release)
#ADD_COMPILE_OPTIONS(-std=c++11 )
#ADD_COMPILE_OPTIONS(-std=c++14 )
#set( CMAKE_CXX_FLAGS "-std=c++11 -O3" )
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread") 
#add_compile_options(-std=c++11) #for arm64
#SET(CMAKE_C_COMPILER aarch64-linux-gnu-gcc)
#SET(CMAKE_CXX_COMPILER aarch64-linux-gnu-g++)
#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)



include_directories(
    ./protocol
    ./task
    ./driver
    ./driver/utils
    ./communication
    )

aux_source_directory(.        SRC_LIST)
aux_source_directory(task     SRC_TASK)
aux_source_directory(communication SRC_COMMUNICATION)
aux_source_directory(protocol SRC_PROTOCOAL)
aux_source_directory(driver   SRC_DRIVER)
aux_source_directory(driver/utils   SRC_UTILS)
aux_source_directory(driver/pciecommmng   SRC_PCIECOMMING)


# Add source to this project's executable.
add_executable (PointsCloud 
                ${SRC_LIST}
                ${SRC_TASK}
                ${SRC_COMMUNICATION}
                ${SRC_PROTOCOAL}
                ${SRC_DRIVER}
                ${SRC_UTILS}
                ${SRC_PCIECOMMING}
                ) 
 

find_package(PCL 1.10 REQUIRED)
include_directories( ${PCL_INCLUDE_DIRS} )
link_directories(${PCL_LIBRARY_DIRS})
#add_definitions(${PCL_DEFINITIONS})

 
#message(${PCL_LIBRARY_DIRS})

#find_package(Eigen3 REQUIRED)
#include_directories("/usr/include/eigen3")



#set(BOOST_ROOT "/usr/include/boost")
#find_package(Boost REQUIRED)
#include_directories(${Boost_INCLUDE_DIRS})
#link_directories(${Boost_LIBRARY_DIRS})
 

#VTK
#find_package(VTK REQUIRED)
#include_directories(${VTK_INCLUDE_DIRS})
#link_directories(${VTK_LIBRARY_DIRS})

#list(REMOVE_ITEM PCL_LIBRARIES "vtkproj4")




# TODO: Add tests and install targets if needed
target_link_libraries(PointsCloud   glog)
target_link_libraries(PointsCloud   pthread dl)
target_link_libraries(PointsCloud   ${PCL_LIBRARIES})

#target_link_libraries(PointsCloud
        #"/usr/lib/x86_64-linux-gnu/libpcl_visualization.so.1.10"
        #libboost_system.so libboost_filesystem.so
        #${VTK_LIBRARIES})




