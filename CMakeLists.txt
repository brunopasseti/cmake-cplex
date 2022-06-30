cmake_minimum_required(VERSION 3.14)

project(sampleCmake)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")
find_package(CPLEX)

if(CPLEX_FOUND)
	add_definitions(-DIL_STD)
else()
	message(FATAL_ERROR "CPLEX not found!")
endif()

add_executable(myprog main.cpp)

target_include_directories(myprog PUBLIC ${CPLEX_INCLUDE_DIRS})
target_link_libraries(myprog PUBLIC ${CPLEX_LIBRARIES})
# set_target_properties(myprog PROPERTIES LINK_FLAGS "-lconcert")
# set_target_properties(myprog PROPERTIES LINK_FLAGS "-lconcert -lilocplex -lcplex -lpthread -ldl")

