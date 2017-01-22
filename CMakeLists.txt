cmake_minimum_required(VERSION 3.1)
option(Coverage "Coverage" OFF)

project(type-erased-storage)

set(DOC_DIR "doc" CACHE STRING "Output directory for the doxygen documentation")

if(Coverage)
  set(CMAKE_BUILD_TYPE Debug)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -coverage")
endif()
  
# Set compiler flags
set(CMAKE_CXX_STANDARD 14)
 
# set up include-directories
include_directories("${PROJECT_SOURCE_DIR}")

add_subdirectory(.)

find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

include(CTest)
enable_testing()

add_executable(${PROJECT_NAME} test.cpp)
target_link_libraries(${PROJECT_NAME} ${GTEST_LIBRARIES} pthread)

