project(q3)

cmake_minimum_required (VERSION 3.5)

# -g allows for gdb debugging
# turn on -03 for best performance
add_definitions(-std=c++11)

set(CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS, "${CXX_FLAGS}")

set(sources ./MPC.cpp)

include_directories(./Eigen-3.3)
include_directories(/usr/local/include)
link_directories(/usr/local/lib)

add_executable(mpc ${sources})

if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
find_package(PythonLibs 2.7)
target_include_directories(mpc PRIVATE ${PYTHON_INCLUDE_DIRS})
target_link_libraries(mpc ipopt ${PYTHON_LIBRARIES})
else()
target_link_libraries(mpc ipopt python)
endif()