cmake_minimum_required(VERSION 3.14)

project(sampleCmake)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")
find_package(CPLEX)

# Cmake module directory
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -DIL_STD -m64 -Wall -Werror")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Og -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DNDEBUG -O3 -flto")
set(CMAKE_INCLUDE_SYSTEM_FLAG_CXX "-isystem ")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/build")
set(LINKER_OPTIONS -flto -Wl,--no-as-needed)

if(CPLEX_FOUND)
	# message(STATUS "Cplex found.")
	# message(STATUS ${CPLEX_INCLUDE_DIRS})
	# message(STATUS ${CPLEX_LIBRARIES})
	add_definitions(-DIL_STD)
else()
	message(FATAL_ERROR "CPLEX not found!")
endif()

add_executable(myprog main.cpp)

# target_link_libraries(myprog dl)
target_include_directories(myprog PUBLIC ${CPLEX_INCLUDE_DIRS})
target_link_libraries(myprog PRIVATE ${CPLEX_LIBRARIES})
target_link_libraries(myprog PRIVATE dl)
message(${CPLEX_LIBRARIES})
# set_target_properties(myprog PROPERTIES LINK_FLAGS "-lconcert")
# set_target_properties(myprog PROPERTIES LINK_FLAGS "-ldl")
